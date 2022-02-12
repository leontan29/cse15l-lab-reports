# Lab Report 3: Bugs and Symptoms

**Part 1: After using the `scp -r . cs15lwi22@ieng6.ucsd.edu:~/markdown-parse` command, we get:**

> MacBook-Pro:markdown-parse leontan$ scp -r . cs15lwi22aji@ieng6.ucsd.edu:~/markdown-parse
MarkdownParseTest.class                       100% 1763    73.9KB/s   00:00    
MarkdownParseTest.java                        100% 2966   144.2KB/s   00:00    
Group-test-file4.md                           100%  109     5.2KB/s   00:00    
Group-test-file.md                            100%   73     3.6KB/s   00:00    
.DS_Store                                     100% 6148   289.8KB/s   00:00    
test-file.md                                  100%   73     3.7KB/s   00:00    
MarkdownParse.java                            100% 2573   123.3KB/s   00:00 
... 

>HEAD                                          100%   30     1.5KB/s   00:00    
main                                          100%   41     2.1KB/s   00:00    
tests                                         100%   41     1.6KB/s   00:00    
main                                          100%   41     2.0KB/s   00:00    
index                                         100% 1352    62.7KB/s   00:00    
packed-refs                                   100%  112     5.9KB/s   00:00    
COMMIT_EDITMSG                                100%   23     1.0KB/s   00:00    
FETCH_HEAD                                    100%  103     4.9KB/s   00:00    
Group-test-file2.md                           100%   69     3.4KB/s   00:00    
test-file2.md                                 100%   69     3.5KB/s   00:00 

 **Part 2: Logging into ieng6 account, and after doing this and compiling and running the tests for your repository**

> ssh cs15lwi22aji@ieng6.ucsd.edu
cd markdown-parse 

> make test
MarkdownParseTest.java:35: 

> error: cannot access MarkdownParse
        ArrayList<String> links = MarkdownParse.getLinks(contents);
                                  ^
  bad class file: ./MarkdownParse.class
    class file has wrong version 60.0, should be 58.0
    Please remove or make sure it appears in the correct subdirectory of the classpath.
1 error
make: *** [MarkdownParseTest.class] Error 1

**Part 3: Now show combining scp, ;, and ssh to copy the whole directory and run the tests in one line.**

Run this command: `scp -r . cs15lwi22aji@ieng6.ucsd.edu:~/markdown-parse; ssh cs15lwi22aji@ieng6.ucsd.edu “cd ~/markdown-parse ; make test”`

The output should look something like this:
(P.S Tutor will get back to me when they figure out what's wrong) 

> bash: “cd: command not found
make: *** No rule to make target `test”'.  Stop.



