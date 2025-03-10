
.. code-block:: bash

  curl -s --user 'api:YOUR_API_KEY' \
     https://api.mailgun.net/v3/domains \
     -F name='YOUR_DOMAIN_NAME' \
     -F smtp_password='supersecret'

.. code-block:: java

 import com.mashape.unirest.http.HttpResponse;
 import com.mashape.unirest.http.JsonNode;
 import com.mashape.unirest.http.Unirest;
 import com.mashape.unirest.http.exceptions.UnirestException;

 public class MGSample {

     // ...

     public static JsonNode addDomain() throws UnirestException {

         HttpResponse<JsonNode> jsonResponse = Unirest.post("https://api.mailgun.net/v3/domains")
             .basicAuth("api", API_KEY)
             .field("name", "YOUR_NEW_DOMAIN_NAME")
             .field("smtp_password", "supersecretpassword")
             .asJson();

         return jsonResponse.getBody();
     }
 }

.. code-block:: php

  # Include the Autoloader (see "Libraries" for install instructions)
  require 'vendor/autoload.php';
  use Mailgun\Mailgun;

  # Instantiate the client.
  $mgClient = Mailgun::create('PRIVATE_API_KEY', 'https://API_HOSTNAME');
  $domain   = 'YOUR_DOMAIN_NAME';

  # Issue the call to the client.
  $result = $mgClient->domains()->create($domain);

.. code-block:: py

 def create_domain():
     return requests.post(
         "https://api.mailgun.net/v3/domains",
         auth=("api", "YOUR_API_KEY"),
         data={"name": "YOUR_DOMAIN_NAME",
               "smtp_password": "supasecret"})

.. code-block:: rb

 def create_domain
   data = {}
   data[:name] = "YOUR_DOMAIN_NAME"
   data[:smtp_password] = "supasecret"
   RestClient.post "https://api:YOUR_API_KEY"\
   "@api.mailgun.net/v3/domains", data
 end

.. code-block:: csharp

 using System;
 using System.IO;
 using RestSharp;
 using RestSharp.Authenticators;

 public class CreateDomainChunk
 {

     public static void Main (string[]args)
     {
         Console.WriteLine (CreateDomain ().Content.ToString ());
     }

     public static IRestResponse CreateDomain ()
     {
         RestClient client = new RestClient ();
         client.BaseUrl = new Uri ("https://api.mailgun.net/v3");
         client.Authenticator =
             new HttpBasicAuthenticator ("api",
                                         "YOUR_API_KEY");
         RestRequest request = new RestRequest ();
         request.Resource = "domains";
         request.AddParameter ("name", "YOUR_NEW_DOMAIN_NAME");
         request.AddParameter ("smtp_password", "supasecret");
         request.Method = Method.POST;
         return client.Execute (request);
     }

 }

.. code-block:: go

 import (
     "context"
     "github.com/mailgun/mailgun-go/v3"
     "time"
 )

 func CreateDomain(domain, apiKey string) (mailgun.DomainResponse, error) {
     mg := mailgun.NewMailgun(domain, apiKey)

     ctx, cancel := context.WithTimeout(context.Background(), time.Second*30)
     defer cancel()

     return mg.CreateDomain(ctx, "example.com", &mailgun.CreateDomainOptions{
         Password: "super_secret",
         SpamAction: mailgun.SpamActionTag,
         Wildcard:   false,
     })
 }

.. code-block:: js

  const formData = require('form-data');
  const Mailgun = require('mailgun.js');

  const mailgun = new Mailgun(formData);

  const client = mailgun.client({ username: 'api', key: 'YOUR_API_KEY' || '' });
  (async () => {
    try {
      const newDomain = await client.domains.create({
      name: "YOUR_NEW_DOMAIN_NAME",
      smtp_login: "alice@YOUR_NEW_DOMAIN_NAME",
      smtp_password: 'secret'
    });
    console.log('newDomain', newDomain);
    } catch (error) {
        console.error(error);
    }
  })();
