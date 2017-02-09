# .NET Developer Assessment

## The purpose of the assessment is to test...
#### Back end skills
* deliver a web API to be consumed by external systems
* design a SQL Server database
* integration with other external APIs

#### Front end skills
* build a front end using HTML and CSS using responsive design
* use JavaScript efficiently

## Please use the following tools as part of your solution:
* Database: SQL Server (any version or edition)
* API: MVC, WebApi or NancyFx
* ORM: NHibernate or Entity Framework
* Testing: xUnit or NUnit
* HTML(5)
* CSS(3) and/or Bootstrap
* JavaScript, jQuery, EmberJS, AngularJS, Knockout

If other tools are used, e.g. Windsor IoC container, please document the tools used, but try and stick to the .NET stack.

## What is expected?
The assessment requires you to develop a C# .NET solution that delivers on the following requirements:

### Front End requirements
A user can search for an artist, see the releases for a specific artist, and add releases to their favourites. A user can see their favourites and update their favourites.

#### Artist search
The front end allows the user to search for an artist. The information is retrieved via the artist search API (see the back end requirements). The search results are displayed in a search results list. 

#### Releases for an artist
From the artists search results list, the user can see all the releases by that artist by clicking on the "Show releases" link. When clicking the link, the releases for the corresponding artist are retrieved from the artist releases API in the back end application and displayed in the releases list. The following release information is shown:
*	Year of release
*	Title of release
*	The label releasing the release
*	Number of tracks on the release
*	Ability to add the release to the user's favourites.

#### Favourite Releases
The user can add a release to their favourites list. The user can also manage their favourites lists.

### Back End Requirements
The back end obviously needs to support the front end requirements. The API you will be writing provides information about artists and their releases and allows users to add and remove releases from their favourites list. The artist information will be stored in a SQL Server database and the release information is provided by the MusicBrainz API.

The Artist Search and Artist Releases endpoints must be developed according to the following specification.
## Artist Search
* ```/artist/search/<search_criteria>/<page_number>/<page_size>``` as a GET. 

  * ```/artist/search/joh``` should return John Coltrane, John Mayer, Johnny Cash, Elton John and John Frusciante
    * The response should contain the following information in JSON
      * Artist name
      * Originating country
      * Aliases for the artist
      * Link to the artist's releases
    * The return data in JSON format should look as follows:
```   
    {
      "results": [
        {
          "uid": "b625448e-bf4a-41c3-a421-72ad46cdb831",
          "name": "John Coltrane",
          "country": "US",
          "alias": [
            "John Coltraine",
            "John William Coltrane"
          ],
          "releasesUrl": "<link to the releases endpoint for this artist>",
        },
        // etc
      ],
      "numberOfSearchResults": 5,
      "page": "1",
      "pageSize": "10",
      "numberOfPages": "1"
  }
```   

The search criteria will be used to search the SQL Server database. The ```page_number``` and ```page_size``` parameters are used for the pagination of the search results. 

The search should return all artists whose name or alias starts with the search criteria. The search should also return pagination information allowing for paging through the search results.

The Excel spreadsheet in the docs folder contains information about 16 artists. The data in the spreasheet needs to be imported into a SQL Server database and used when searching for artists

## Artist Releases
* ```/artist/<artist_id>/releases``` as a GET. This endpoint will return all the releases for a selected artist where the artist_id uniquely identifies an artist in the SQL Server database and MusicBrainz API.

  * ```/artist/6c44e9c22-ef82-4a77-9bcd-af6c958446d6/releases``` will return the first 10 releases from Mumford & Sons.
    * The response should contain the following information in JSON
      * Release Id
      * Title of release
      * Status release
      * Label which released the release
      * Number of tracks on the release
      * Year of release
      * List of artist collabrating on the release
    * The return data in JSON format should look as follows:
  ```
      {
        "releases": [
          {
            "releaseId": "9cc88413-d456-4b96-a0c1-09fa6cc2cf88",
            "title": "iTunes Festival: London 2010" ,
            "status": "Official",
            "label": "Gentlemen of the Road",
            "numberOfTracks": "8",
            "yearOfRelease": "2010",
            "otherArtists": [
              {
                "id": "a015074b-e109-412d-9f7b-170b80a0ebbd",
                "name": "Dharohar Project"
              },
              {
                "id": "cd9713d6-6e5f-4143-9412-4d12b7bd47f2",
                "name": "Laura Marling"
              }
            ]     
          },
          //etc
        ]
      }
  ```

## Supporting documentation
Documents can be found in the docs folder of the repository

* An Excel spreadsheet with artist information. This information is used for searching and contains the identifier to link to MusicBrainz.
* The MusicBrainz API is well documented and the information can be found at http://musicbrainz.org/doc/Development/XML_Web_Service/Version_2/Search

## What should be part of your solution?
* SQL Server scripts to create the database and other database objects required by the solution
* SQL Server scripts to populate the database with artist information (based on the data in the Excel spreadsheet). Basically a number of INSERT statements to populate the database
* Any other documentation needed to execute your solution


## How will the technical assessment be evaluated?
* The database scripts provided will be run against a local SQL Server database (we'll update the connection string to point to the appropriate database)
* The solution will be installed in IIS
* The solution will be opened in the Chrome browser and the functionality described above will be tested. Both positive and negative tests will be done against the solution.
* The two endpoints will be invoked, using Postman (https://www.getpostman.com/) to test the results returned. Both positive and negative tests will be executed
* The code will evaluated for clarity, design and readability.
* If any tests are part of the submitted solution, the tests will be run the test the solution. The tests will be evaluated to verify the quality of the tests.
* Responsive layouts will be simulated using Chrome's developer tools.

## How do I submit my solution?
Send us a link to your repository by emailing the person who sent you the assessment.

## Questions or comments
Please use the issues functionality on Github. All questions will be answered via Github.
