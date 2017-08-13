# githubtoaws
Overview/Assumptions: this project aims to build a process to search through specific GitHub repositories and extract contents of the meta file(s) and upload to AWS S3. The code is incomplete; however, should be not too far from being completed.

Code Example: See Initial Commit for code file (AWS.GitHubtoAWS.docx). 

Testing: Import and run the following .jar files from a Java IDE (I used eclipse) in the following manner:
URLConnectionReader - Search and return the git_url for the file(s) 
URLConnectionReaderContent - Search the git_url and return the content of the 
UploadObjectSingleOperation - Create a file of repo.meta data and upload the same to 
