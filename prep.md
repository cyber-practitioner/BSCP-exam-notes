for URl blacklist bpyass you need to understadn the underlying server through the error that you get when you upload a php file
afer that based on the web server you need to upload the server configuration .htaccess with content type: text/plain and ADDDtype application/php to .qaz (or any extension name you choose)
after receive 200 OK on this request you uplaod another PHp file with efault config type however use the extension it was mapped with .htaccess file with the php code to access carlos' directory
then access the location of that file 

hacking implicit flow
check for user token in a POST request after logging in as a valid user but the application does not validate the cookoe so in the reponse you change 

{"email":"wiener@hotdog.com","username":"wiener","token":"7obMudOkxiQkB7HJImGIx6WqQv1LsbasSt1lihLcJ10"}
to 

{"email":"carlos@carlos-montoya.net","username":"carlos","token":"7obMudOkxiQkB7HJImGIx6WqQv1LsbasSt1lihLcJ10"}