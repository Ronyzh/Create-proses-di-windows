# Create-proses-di-windows
Tugas 2 Sistem Operasi

#include <stdio.h>
#include <windows.h>

int main(VOID)
{
STARUPINFO si;
PROCESS_INFORMATION pi;

  /* allocate memory */
  ZeroMemory(&si, sizeof(si));
  si.cb = sizeof(si);
  ZeroMemory(&pi, sizeof(pi));
  
  /* cread child process */
  if (!CreateProcess(NULL, /*use command line */
    "C:\\WINDOWS\\system32\\mspaint.exe", /* command */
    NULL, /* don't inherit process handle */
    NULL, /* don't inherit thread handle */
    FALSE, /* disable handle inheritance */
    0, /* no creating flags */
    NULL, /* use parent's enviroment block */
    NULL, /* use parent's exiting directory */
    &si,
    &pi))
   {
    fprintf(stderr, "Create Process Failed");
    return -1;
   }
   /* parent will wait for the child to complete */
   WaitForSingleObject(pi.hProcess, INFINITE);
   printf("Child Complete");
   
   /* close handle */
   CloseHandle(pi.hProcess);
   CloseHandle(pi.hThread);
}
    
