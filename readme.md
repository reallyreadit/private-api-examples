# Readup Private API Examples
## API Access
Readup doesn't have a public API yet but you can still poke around programmatically if you're so inclined. Readup captures a lot of interesting data and we're eager to build a proper public API for our users but in the mean time you can still make use of our private API using an HTTP client and the examples below.

**Please keep in mind these APIs absolutely WILL change in the future!** Also feel free to submit a pull request with any additional examples or corrections. Thanks!
## Accessing Your Readup Reading History
1. First you need to obtain an authentication cookie from Readup. Replace `EMAIL_ADDRESS` and `PASSWORD` with your Readup credentials:

    ```curl --request POST --data "{\"email\":\"EMAIL_ADDRESS\",\"password\":\"PASSWORD\"}" --header "Content-Type: application/json" --header "X-Readup-Client: web/app/client#Browser@1.32.0" --cookie-jar readup-auth-cookie.txt https://api.readup.com/UserAccounts/SignIn```

	 **This command will create a text file named "readup-auth-cookie.txt" in your current working directory containing your authentication cookie. Be sure to properly safeguard this file!**

	 You may need to change the JSON data escaping depending on your operating system or terminal software. See this StackOverflow question for more info: [How do I POST JSON data with cURL?](https://stackoverflow.com/questions/7172784/how-do-i-post-json-data-with-curl)

2. Then you can make a request to list your reading history using those credentials:

    ```curl --request GET --header "X-Readup-Client: web/app/client#Browser@1.32.0" --cookie readup-auth-cookie.txt https://api.readup.com/Articles/ListHistory?pageNumber=1```

    Article info will be returned in JSON format. Page size is fixed at 40 articles per page. In addition to setting pageNumber you can also specify minLength and/or maxLength (in minutes) in order to limit results by article length.