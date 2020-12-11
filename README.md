## Description

This is an implementation of an FTP client running on the command line.


## Approach

To implement the client the code is broken into segments for connecting to the ftp server, reading the command line, sending the proper codes to the server, and sending data through the data channel.

### FTP Connection and Command Line

* Using the argparse and urlparse library to read from the command line
* argparse with only two arguments. The parameter argument takes a varied amount and ensures the correct amount for the given operation
* NOTE: global variable 'MSG' to append and gather the commands to send to the FTP server
* While recieving data from the FTP server look for codes that indicate passive mode or goodbye

### Operations and helpers

* The command line, using if statements to find which operation case
* Corresponding operation function that would append to specific codes to the MSG variable

### Data Channel

* FTP client looks for 227 passive mode code
* Helper functions to break down the 6 numbers into a proper ip and port
* Connect to the data channel using the ip and port that was found
* Operations that require the data channel call to connect and add codes

## Challenges

Aside from the ls command the cp and mv would hang after entering the passive mode. I could not solve how to send the file over the data channel. Although I tried to send the file as bytes there seems to be an element I am missing in order for the data to properly upload throught the channel. The data channel would hang and I did not recieve any insight for if it failed or it succeeded the file transfer.

## Testing 

examples:

./3700ftp ls ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/

./3700ftp rm ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/hello.txt

./3700ftp mkdir ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/newDir

./3700ftp rmdir ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/test2

./3700ftp mv test/example.txt ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/

./3700ftp mv ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/ test/example.txt

./3700ftp cp test/example.txt ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/

./3700ftp cp ftp://josephpr:uY0PfJNgQ98VnF5IbHaL@3700.network:21/ test/example.txt
