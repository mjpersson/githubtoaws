GitHub to AWS

URLConnectionReader.jar
package ghdownload;
import java.net.*;
import java.io.*;
import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class URLConnectionReader
{

       public static void main(String[] args) throws Exception {

              String inputLine;
              URL github = new URL("https://api.github.com/search/code?q=user:byu-oit+extension:meta+filename:repo+fork:only");
              URLConnection uc = github.openConnection();
              BufferedReader in = new BufferedReader(
              new InputStreamReader(uc.getInputStream()));
              while((inputLine = in.readLine()) != null) {
                     Pattern pattern = Pattern.compile("git_url\":(.*?),");
                     Matcher matcher = pattern.matcher(inputLine);

                     while (matcher.find()) {

                           //inputLine=(matcher.group(1));
                           //System.out.println(matcher.group(1));
                           inputLine = "https://api.github.com/repositories/51163126/git/blobs/290060a4e961e627baa8189db6afe0a40936e003";
                     }
              }
                     in.close();
       }
} 


URLConnectionReaderContent.jar

package ghdownload;
import java.net.*;
import java.io.*;
import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class URLConnectionReaderContent {

       public static void main(String[] args) throws Exception {

              String inputLine = "";
              //URLConnectionReader ucr = new URLConnectionReader();
              //ucr.main(args);
              //ucr.main(args).toString();
            
              URL github = new URL("https://api.github.com/repositories/51163126/git/blobs/290060a4e961e627baa8189db6afe0a40936e003");
              URLConnection uc = github.openConnection();
              BufferedReader in = new BufferedReader(
              new InputStreamReader(uc.getInputStream()));
              while((inputLine = in.readLine()) != null) {
                     Pattern pattern = Pattern.compile("content\":\"(.*?)\",");
                     Matcher matcher = pattern.matcher(inputLine);
                     while (matcher.find()) {
                           //public void printGitURL() {
                           inputLine=(matcher.group(1));
                           //System.out.println(matcher.group(1));
                     }
              }
              in.close();
       }           
}


UploadObjectSingleOperation.jar

package awsupload;
import java.net.*;
import java.io.*;
/*import java.io.BufferedReader;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.util.Arrays;
import java.util.function.Function;*/

import com.amazonaws.AmazonClientException;
import com.amazonaws.AmazonServiceException;
import com.amazonaws.auth.AWSCredentials;
import com.amazonaws.auth.BasicAWSCredentials;
import com.amazonaws.auth.profile.ProfileCredentialsProvider;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3Client;
import com.amazonaws.services.s3.model.DeleteObjectRequest;
import com.amazonaws.services.s3.model.GetObjectRequest;
import com.amazonaws.services.s3.model.PutObjectRequest;
import com.amazonaws.services.s3.model.S3Object;
import com.amazonaws.services.s3.model.S3ObjectInputStream;
import ghdownload.URLConnectionReader;

public class UploadObjectSingleOperation {
                private static String bucketName    = "githubtoaws";
                private static String keyName     = "repo.meta";
                private static String inputLine = "";
                //private static String uploadFileAPI        = inputLine;
                             
                                                //"https://api.github.com/search/code?q=user:byu-oit+extension:meta+filename:repo";
                //private static String uploadFileName   = "/Users/Family PC/Desktop/BYU Project/dsktptoaws.txt";         
         
                void uploadfile(AWSCredentials credentials) throws Exception
                {
                                                AmazonS3 s3client = new AmazonS3Client(credentials);                 
                                                try {
                                                                System.out.println("Uploading a new object to S3 from a file\n");                                                   
                                                                File file = new File("repo.meta");
                                                                FileWriter fileWriter = new FileWriter(file);
                                                                fileWriter.write(inputLine);
                                                                fileWriter.flush();
                                                                fileWriter.close();
                                                                s3client.putObject(new PutObjectRequest(
                                                                                                bucketName, keyName, file));
                                                }
                                                catch (AmazonServiceException ase) {
                                                                System.out.println("AmazonServiceException" +
                                                                                                "Request arrived, but rejected by Amazon S3.");
                                                                System.out.println("Error Message:     " + ase.getMessage());
                                                                System.out.println("HTTP Status Code:  " + ase.getStatusCode());
                                                                System.out.println("AWS Error Code:    " + ase.getErrorCode());
                                                                System.out.println("Error Type:        " + ase.getErrorType());
                                                                System.out.println("Request ID:        " + ase.getRequestId());
                                                }
                                                catch (AmazonClientException ace) {
                                                                System.out.println("AmazonClientException" +
                                                                                                "Internal Error: Amazon S3 is not reachable.");
                                                                System.out.println("Error Message:        " + ace.getMessage());
                                                }
                }
                void deletefile(AWSCredentials credentials1)
                {
                                                AmazonS3 s3client = new AmazonS3Client(credentials1);
                                                try {
                                                                s3client.deleteObject(new DeleteObjectRequest(bucketName, keyName));
                                                }
                                                catch (AmazonServiceException ase) {
                                                                System.out.println("AmazonServiceException: request rejected by Amazon S3.");
                                                                System.out.println("Error Message:          " + ase.getMessage());
                                                                System.out.println("HTTP Status Code:       " + ase.getStatusCode());
                                                                System.out.println("AWS Error Code:         " + ase.getErrorCode());
                                                                System.out.println("Error Type:             " + ase.getErrorType());
                                                                System.out.println("Request ID:             " + ase.getRequestId());
                                                }
                                                catch (AmazonClientException ace) {
                                                                System.out.println("AmazonClientException: Amazon S3 is not reachable.");
                                                                System.out.println("Error Message:          " + ace.getMessage());
                                                }
                }
                downloadfile(AWSCredentials credentials2) throws IOException
                {
                                                AmazonS3 s3client = new AmazonS3Client(credentials2);
                                                try{
                                                                System.out.println("Downloading Object");

                                                                S3Object s3object = s3client.getObject(new GetObjectRequest(
                                                                                                bucketName, keyName));
                                                                System.out.println("Content-Type:          " + s3object.getObjectMetadata().getContentType());
                                                                InputStream input = s3object.getObjectContent();
                                                                BufferedReader reader = new BufferedReader(new InputStreamReader(input));
                                                                while (true) {
                                                                                String line = reader.readLine();
                                                                                if(line == null) break;                                                                              
                                                                                System.out.println("       " + line);
                                                                }
                                                                System.out.println();
                                                }
                                                catch (AmazonServiceException ase) {
                                                                System.out.println("AmazonServiceException: request rejected by Amazon S3.");
                                                                System.out.println("Error Message:          " + ase.getMessage());
                                                                System.out.println("HTTP Status Code:       " + ase.getStatusCode());
                                                                System.out.println("AWS Error Code:         " + ase.getErrorCode());
                                                                System.out.println("Error Type:             " + ase.getErrorType());
                                                                System.out.println("Request ID:             " + ase.getRequestId());
                                                }
                                                catch (AmazonClientException ace) {
                                                                System.out.println("AmazonClientException: Amazon S3 is not reachable.");
                                                                System.out.println("Error Message:          " + ace.getMessage());
                                                }                                                                             
                }
 
                public static void main(String[] args) throws Exception {
                                //String inputLine = "";
                                ghdownload.URLConnectionReaderContent ucrc = new ghdownload.URLConnectionReaderContent();
                                ucrc.main(args);
                                AWSCredentials Credentials = new BasicAWSCredentials(
                                                                "AKIAI54PW2ITUL2UUBAQ",
                                                                "CUI6hF2sQMvPHWrsTbdRxeA3V0HNDw+eRM5FX5Zs");
                                UploadObjectSingleOperation s3client = new UploadObjectSingleOperation();
                                s3client.uploadfile(Credentials);
                                //s3client.deletefile(Credentials);
                                //s3client.downloadfile(Credentials);\              
                }
}

