.. code-block:: bash

  curl -s --user 'api:YOUR_API_KEY' -X PUT \
    https://api.mailgun.net/v3/YOUR_DOMAIN_NAME/templates/TEMPLATE_NAME/versions/VERSION_TAG \
    -F template='{{fname}} {{lname}}' \
    -F comment='Updated version comment' \
    -F active='yes'

.. code-block:: java

 import com.mashape.unirest.http.HttpResponse;
 import com.mashape.unirest.http.JsonNode;
 import com.mashape.unirest.http.Unirest;
 import com.mashape.unirest.http.exceptions.UnirestException;

 public class MGSample {

      // ...

     public static JsonNode UpdateVersion() throws UnirestException {

         HttpResponse <JsonNode> request = Unirest.put("https://api.mailgun.net/v3/" + YOUR_DOMAIN_NAME + "/templates/TEMPLATE_NAME/versions/VERSION_TAG")
            .basicAuth("api", API_KEY)
            .field("template", "{{fname}} {{lname}}")
            .field("comment", "Updated version comment")
            .field("active", "yes")
            .asJson();

         return request.getBody();
     }
 }

.. code-block:: php

  # Currently, the PHP SDK does not support the Templates endpoint.
  # Consider using the following php curl function.
  function update_template_version() {
    $params =   array(
      'template' => '{{fname}} {{lname}}',
      'comment' => 'Updated version comment',
      'active' => 'yes'
    );

    $ch = curl_init();

    curl_setopt($ch, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
    curl_setopt($ch, CURLOPT_USERPWD, 'api:PRIVATE_API_KEY');
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

    curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'PUT');
    curl_setopt($ch, CURLOPT_URL, 'https://api.mailgun.net/v3/YOUR_DOMAIN_NAME/templates/TEMPLATE_NAME/versions/VERSION_TAG');
    curl_setopt($ch, CURLOPT_POSTFIELDS, $params);

    $result = curl_exec($ch);
    curl_close($ch);

    return $result;
  }


.. code-block:: py

 def update_version():
     return requests.put(
         "https://api.mailgun.net/v3/YOUR_DOMAIN_NAME/templates/TEMPLATE_NAME/versions/VERSION_TAG",
         auth=("api", "YOUR_API_KEY"),
         data={'template': '{{fname}} {{lname}}',
               'comment': 'Updated version comment',
               'active': 'yes'})

.. code-block:: rb

 def update_version:
   RestClient.put "https://api:YOUR_API_KEY"\
   "@api.mailgun.net/v3/YOUR_DOMAIN_NAME/templates/TEMPLATE_NAME/versions/VERSION_TAG",
   :template => '{{fname}} {{lname}}',
   :comment => 'Updated version comment',
   :active => 'yes'
 end

.. code-block:: csharp

 using System;
 using System.IO;
 using RestSharp;
 using RestSharp.Authenticators;

 public class UpdateVersionChunk
 {

     public static void Main (string[] args)
     {
         Console.WriteLine (UpdateVersion ().Content.ToString ());
     }

     public static IRestResponse UpdateVersion ()
     {
         RestClient client = new RestClient ();
         client.BaseUrl = new Uri ("https://api.mailgun.net/v3");
         client.Authenticator =
             new HttpBasicAuthenticator ("api",
                                         "YOUR_API_KEY");
         RestRequest request = new RestRequest ();
         request.Resource = "{domain}/templates/{name}/versions/{tag}";
         request.AddParameter ("domain", "YOUR_DOMAIN_NAME", ParameterType.UrlSegment);
         request.AddParameter ("name", "TEMPLATE_NAME", ParameterType.UrlSegment);
         request.AddParameter ("tag", "VERSION_TAG", ParameterType.UrlSegment);
         request.AddParameter ("template", "{{fname}} {{lname}}");
         request.AddParameter ("comment", "Updated version comment");
         request.AddParameter ("active", "yes");
         request.Method = Method.PUT;
         return client.Execute (request);
     }

 }

.. code-block:: go

    import (
        "context"
        "github.com/mailgun/mailgun-go/v3"
        "time"
    )

    func UpdateTemplateVersion(domain, apiKey string) error {
        mg := mailgun.NewMailgun(domain, apiKey)

        ctx, cancel := context.WithTimeout(context.Background(), time.Second*30)
        defer cancel()

        return mg.UpdateTemplateVersion(ctx, "TEMPLATE_NAME", &mailgun.TemplateVersion{
            Comment: "Add a comment to the template and make it 'active'",
            Tag:     "VERSION_TAG",
            Active:  true,
        })
    }

.. code-block:: js

  const DOMAIN = 'YOUR_DOMAIN_NAME';
  const TEMPLATE_NAME = 'template.name';
  const VERSION_TAG = 'v2';

  const formData = require('form-data');
  const Mailgun = require('mailgun.js');

  const mailgun = new Mailgun(formData);

  const client = mailgun.client({ username: 'api', key: 'YOUR_API_KEY' || '' });
  (async () => {
    try {
      const updatedTemplateVersion = await client.domains.domainTemplates.updateVersion(
        DOMAIN,
        TEMPLATE_NAME,
        VERSION_TAG,
        {
        template: '{{fname}} {{lname}}',
        comment: "Updated version comment",
        active: 'yes'
        }
      );
      console.log('updatedTemplateVersion', updatedTemplateVersion);
    } catch (error) {
      console.error(error);
    }
  })();
