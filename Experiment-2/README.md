# Experiment 2: Install a C Compiler in the Virtual Machine Created Using VirtualBox and Execute a Simple Program

## Aim
To install a C compiler in the virtual machine created using VirtualBox and execute a simple program.

## Procedure

### Part A: Import the Ubuntu virtual machine
1. Open VirtualBox.
2. Go to **File** > **Import Appliance**.
3. Browse and select the `ubuntu_gt6.ova` file.
4. Go to **Settings**, select **USB** and choose **USB 1.1**.
5. Start the `ubuntu_gt6` virtual machine.

### Part B: Write and run the C program
1. Open the terminal.
2. Go to the working directory:
```bash
   cd /opt/axis2/axis2-1.7.3/bin
```
3. Create the C file:
```bash
   gedit first.c
```
4. Type the C program and save it:
```c
   #include <stdio.h>

   int main()
   {
       int a, b, sum;
       printf("Enter two number:\n");
       scanf("%d %d", &a, &b);
       sum = a + b;
       printf("The addition of a and b:%d\n", sum);
       return 0;
   }
```
5. Compile the program:
```bash
   gcc first.c
```
6. Run the program:
```bash
   ./a.out
```

## Output
```
Enter two number:
65
23
The addition of a and b:88
```

## Result
The C compiler (`gcc`) was used in the Ubuntu virtual machine, and a simple C program was compiled and executed successfully.

<img width="695" height="547" alt="Screenshot 2026-10-07 195337" src="https://github.com/user-attachments/assets/7204b822-8a5c-4f29-be1c-267674c30193" />

<img width="822" height="482" alt="Screenshot 2026-10-07 195615" src="https://github.com/user-attachments/assets/be0a5083-5217-4a68-a819-957c2b2348b0" />


