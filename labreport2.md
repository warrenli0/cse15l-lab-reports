# Warren Li - CSE 15L Lab Report 2

## Part 1
StringServer.java:
```Java
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    private StringBuilder messages = new StringBuilder();
    private int messageCount = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Messages: " + messages.toString());
        } else if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters.length == 2 && parameters[0].equals("s")) {
                messageCount++;
                messages.append(messageCount).append(". ").append(parameters[1]).append("\n");
                return messages.toString();
            } else {
                return "Invalid request!";
            }
        } else {
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
1. 
<img width="450" alt="Screen Shot 2023-10-21 at 11 37 44 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/29f16d80-6b33-485e-afee-a36c239c1ce9"><br>
In the screenshot, the `handleRequest` function is being called. The arguments for the function is the `URI url`, which in this case was `/add-message?s=Hello`. The values in the class were at their initial empty state before the request, and after the request, messages became `1. Hello\n` and `messageCount` became `1`.

2.
<img width="525" alt="Screen Shot 2023-10-21 at 11 38 22 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/36563533-e6a5-44c8-8585-83075d26d9d8"><br>
In the screenshot, the `handleRequest` function is being called. The arguments for the function is the `URI url`, which in this case was `/add-message?s=How%20are%20you`. The values in the class were at the state from the previous screenshot, and after the request, messages became `1. Hello\n 2. How are you\n` and `messageCount` became `2`.

## Part 2
Path to private key on local computer:
<img width="628" alt="Screen Shot 2023-10-21 at 11 45 48 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/57ab2ce1-3425-46cc-bc0e-c2c83fafea06"><br>

Path to public key on ieng6:
<img width="324" alt="Screen Shot 2023-10-21 at 11 49 15 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/e26915f1-806a-4b41-8d06-d8b8855b0868"><br>

No login required for ssh:
<img width="766" alt="Screen Shot 2023-10-21 at 11 48 07 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/4bb6da96-19e2-4800-a694-21d2569f0a61"><br>


## Part 3
Something that I learned in Lab 3 was using SSH keys for easy access to the server without login. I knew how to use SSH and use key-pairs before but the process of skipping the login was new to me since I never manually copied the keys over to the server before.
