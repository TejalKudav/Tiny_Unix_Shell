Tiny_Unix_Shell
===============
Simple Unix shell program that supports job control and I/O redirection.
 
tsh shell has the following features:

• The prompt is the string “tsh> ”.

• The command line typed by the user consists of a name and zero or more arguments, all sepa- rated by one or more spaces. If name is a built-in command, then tsh handles it immediately and waits for the next command line. Otherwise, tsh assumes that name is the path of an executable file, which it loads and runs in the context of an initial child process (In this context, the term job refers to this initial child process). If you are running system programs like ls, you will need to enter the full path (in this case /bin/ls) because the shell does not have search paths.

• tsh does not support pipes (|), but supports I/O redirection (“<” and “>”), for instance: tsh> /bin/cat < foo > bar
Your shell supports both input and output redirection in the same command line.

• Typing ctrl-c (ctrl-z) causes a SIGINT (SIGTSTP) signal to be sent to the current fore- ground job, as well as any descendants of that job (e.g., any child processes that it forked). If there is no foreground job, then the signal has no effect.

• If the command line ends with an ampersand &, then tsh runs the job in the background. Otherwise, it runs the job in the foreground.

• Each job can be identified by either a process ID (PID) or a job ID (JID), which is a positive integer assigned by tsh. JIDs should be denoted on the command line by the prefix ’%’. For example, “%5” denotes JID 5, and “5” denotes PID 5.

• tsh supports the following built-in commands:
– The quit command terminates the shell.
– The jobs command lists all background jobs.
– The bg job command restarts job by sending it a SIGCONT signal, and then runs it in the background. The job argument can be either a PID or a JID.
– The fg job command restarts job by sending it a SIGCONT signal, and then runs it in the foreground. The job argument can be either a PID or a JID.
• Your
shell should be able to redirect the output from the jobs built-in command. For example
tsh> jobs > foo
• tsh should reap all of its zombie children. If any job terminates because it receives a signal that it didn’t catch, then tsh should recognize this event and print a message with the job’s PID and a description of the offending signal.