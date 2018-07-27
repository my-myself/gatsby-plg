# gatsby-starter-plg v. 0.2
The Gatsby starter.

## How to Install

Make sure that you have the Gatsby CLI program installed:
```sh
npm install --global gatsby-cli
```

And run from your CLI:
```sh
gatsby new gatsby-example-site
```

Then you can run it by:
```sh
cd gatsby-example-site
gatsby develop
```

## How to use

When you create a new workspace, *id* of the created workspace will be in the address bar, for example:
`https://<YOUR_CMS_LINK>.com/workspace/2`

where *2* necessary for us *id*, which we copy and paste into the file gatsby-node.js, in the line:
`const fetchTextTestField = () => axios.get (`<YOUR_CMS_LINK>/workspace=2`); `

Then when you create any type of field in your CMS you take a flag/slug like a name of the field.
when you create any field in your cms system, you get a flag with the same name that was given to the field. Next, you need to copy this flag, run the project (if it is not running), and follow the link that the terminal will give, most often it is: open the graphql and check whether under the given flag you can "pull out" the field information.
'http: // localhost: 8000 /' - to view the site
'http: // localhost: 8000 / ___ graphql' - for editing queries,
after which you need to go to the graphql and enter the following in the field of the graphical queries:
```
query SiteCmsQuery {
    allDataCms {
      edges {
        node {
          allData {
   			data{
   			en {
              header_text
              subtitle
              <YOUR_FLAG>
              etc..
              }
            }
          }
        }
      }
    }
  }
}
```
if you add a "repeater" field then your flag will look a little different:

```
...
<YOUR_FLAG> {
  <FIELDS>
  <FIELDS>
  <FIELDS>
}
...

```

and then collecting everything together, it will look like this:

```
query SiteCmsQuery {
    allDataCms {
      edges {
        node {
          allData {
   			data{
   			en {
              header_text
              subtitle
              <YOUR_FLAG>
              <YOUR_FLAG> {
                <FIELDS>
                <FIELDS>
                <FIELDS>
              }
              etc..
              }
            }
          }
        }
      }
    }
  }
}

```
after you add everything you need to the graphql, click the Execute Query (Ctrl-Enter) button, in the block on the right you will see the structure of the fact that the flags are "pulled out" from your CMS.
if an error has occurred then you follow to check the correct spelling of the request. If the error is not lost, it is better to refer to the official Gatsby documentation.

If everything went well, you need to copy the query and paste it into the page you need.
for insertion on the page is used:
```
export const query = graphql`<YOUR_QUERY>`

```

in order to display the required field on the page, the base component of the page with GraphQL query might look something like this:

```
import React from "react";

export default ({ data }) => (
  <div>
    <h1>About {data.site.siteMetadata.title}</h1>
    <p>We're a very cool website you should return to often.</p>
  </div>
);

export const query = graphql`
  query AboutQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`;
```
or if you want to output text from a field, for example, an editor(wysiwyg in CMS) on checkbox(bool), then a basic page component with a GraphQL query might look something like this

```
import React from "react";

export default ({ data }) => (
  <div>
    <div>{node.allData.data.en.header_text}</div>
    <p>We're a very cool website you should return to often.</p>
    *<div dangerouslySetInnerHTML={{__html: node.allData.data.en.teeest2}}></div>*
  </div>
);

export const query = graphql`
  query SiteCmsQuery {
      allDataCms {
        edges {
          node {
            allData {
              data{
                en {
                  header_text
                  teeest2
                }
              }
            }
          }
        }
      }
    }
`;

```
after this, you need to restart the project.
and open the page on the local server. If you did everything correctly, the page should display the data that you entered in the fields of your CMS.

If you have any questions or difficulties, you can read more details https://www.gatsbyjs.org/docs/querying-with-graphql/ and https://www.gatsbyjs.org/docs/building-with-components/

## How to Deploy

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/gatsbyjs/gatsby-starter-default)

