# Experiment 7: Implementation of Thread Based Image Processing Application in Microsoft Azure

## Aim
To implement a thread based image processing application in Microsoft Azure.

## Prerequisites
- A Microsoft Azure account
- Python 3 installed
- A few sample image files (JPEG)

## Procedure

### Step 1: Create an Azure account
1. Go to Microsoft Azure.
2. Sign in or create a new account.
3. Open the Azure Portal.

### Step 2: Create a Storage Account
1. In the Azure Portal, search for **Storage Accounts**.
2. Click **Create**.
3. Fill in the details:
   - **Resource Group:** Create new
   - **Storage Account Name:** `imagestorage123`
   - **Region:** Choose the nearest (e.g., Central India)
4. Click **Review + Create** > **Create**.

### Step 3: Create a Blob Container
1. Open the created Storage Account.
2. Go to **Containers**.
3. Click **+ Container**.
4. Name: `images`
5. Access level: **Private**
6. Click **Create**.

### Step 4: Upload sample images
1. Open the `images` container.
2. Click **Upload**.
3. Select multiple image files.
4. Click **Upload**.

### Step 5: Get the connection string
1. Go to **Access Keys** in the Storage Account.
2. Copy the **Connection String**.
3. Save it for use in the code.

### Step 6: Install the required libraries
```bash
pip install azure-storage-blob pillow
```

### Step 7: Write the multithreaded Python code
Create a file named `app.py` with the following code:

```python
import threading
from azure.storage.blob import BlobServiceClient
from PIL import Image
import io

# Azure connection
connection_string = "YOUR_CONNECTION_STRING"
container_name = "images"
blob_service_client = BlobServiceClient.from_connection_string(connection_string)


def process_image(blob_name):
    blob_client = blob_service_client.get_blob_client(
        container=container_name, blob=blob_name
    )

    # Download image
    data = blob_client.download_blob().readall()
    stream = io.BytesIO(data)

    # Open and process image
    img = Image.open(stream)
    img = img.resize((200, 200))  # Resize

    # Save processed image
    output = io.BytesIO()
    img.save(output, format='JPEG')
    output.seek(0)

    # Upload processed image
    new_name = "processed_" + blob_name
    blob_service_client.get_blob_client(
        container=container_name, blob=new_name
    ).upload_blob(output, overwrite=True)


def main():
    container_client = blob_service_client.get_container_client(container_name)
    blobs = container_client.list_blobs()

    threads = []

    # Create threads
    for blob in blobs:
        t = threading.Thread(target=process_image, args=(blob.name,))
        threads.append(t)
        t.start()

    # Wait for completion
    for t in threads:
        t.join()

    print("All images processed successfully")


if __name__ == "__main__":
    main()
```

### Step 8: Run the application
1. Replace `"YOUR_CONNECTION_STRING"` with the actual connection string.
2. Run the script:
```bash
   python app.py
```

### Step 9: Verify the output
1. Go back to the Azure Portal.
2. Open the Blob Container (`images`).
3. Check for the new files:
   - `processed_image1.jpg`
   - `processed_image2.jpg`

## Output
Terminal output:
```
All images processed successfully
```

The `images` container now contains a resized (200 x 200) copy of each uploaded image, with the prefix `processed_`.

## Result
A thread based image processing application was successfully implemented in Microsoft Azure. Each image was processed in its own thread, and the resized images were stored back in the Blob container.