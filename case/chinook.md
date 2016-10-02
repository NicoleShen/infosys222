# <i class="fa fa-database"></i> INFOSYS 222
### Case: Chinook
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222) | <i class="fa fa-calendar-o"></i> 2016-09-19 | <i class="fa fa-calendar-plus-o"></i> 2016-10-03



## Background
- [Chinook](http://chinookdatabase.codeplex.com/) is a sample database being commonly used for demos and testing purposes on multiple products including SQLite. It is an open source project

- The database can be created by running a single [SQL script](https://raw.githubusercontent.com/johnny723/infosys222/master/case/chinook.sql)

- The company Chinook runs a business of selling tracks and albums of music and video online. The database manages all the transactions, and all relevant information related to the products and customers



## Specification
- The following specification captures the Chinook database schema through all the CREATE TABLE statements that build up the database:

  - Album
  - Artist
  - Customer
  - Employee
  - Genre
  - Invoice
  - InvoiceLine
  - MediaType
  - PlayList
  - PlayListTrack
  - Track


## Album
```
CREATE TABLE Album
(
    AlbumID INTEGER PRIMARY KEY NOT NULL,
    Title TEXT NOT NULL,
    ArtistID INTEGER NOT NULL,
    FOREIGN KEY (ArtistID) REFERENCES Artist (ArtistID)
		ON DELETE NO ACTION ON UPDATE NO ACTION
);
```


## Artist
```
CREATE TABLE Artist
(
    ArtistID INTEGER PRIMARY KEY NOT NULL,
    Name TEXT
);
```


## Customer
```
CREATE TABLE Customer
(
    CustomerID INTEGER PRIMARY KEY NOT NULL,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Company TEXT,
    Address TEXT,
    City TEXT,
    State TEXT,
    Country TEXT,
    PostalCode TEXT,
    Phone TEXT,
    Fax TEXT,
    Email TEXT NOT NULL,
    SupportRepID INTEGER,
    FOREIGN KEY (SupportRepID) REFERENCES Employee (EmployeeID)
		ON DELETE NO ACTION ON UPDATE NO ACTION
);
```
<!-- .element: style="font-size:85%" -->


## Employee
```
CREATE TABLE Employee
(
    EmployeeID INTEGER PRIMARY KEY NOT NULL,
    LastName TEXT NOT NULL,
    FirstName TEXT NOT NULL,
    Title TEXT,
    ReportsTo INTEGER,
    BirthDate DATE,
    HireDate DATE,
    Address TEXT,
    City TEXT,
    State TEXT,
    Country TEXT,
    PostalCode TEXT,
    Phone TEXT,
    Fax TEXT,
    Email TEXT,
    FOREIGN KEY (ReportsTo) REFERENCES Employee (EmployeeID)
		ON DELETE NO ACTION ON UPDATE NO ACTION
);
```
<!-- .element: style="font-size:75%" -->


## Genre
```
CREATE TABLE Genre
(
    GenreID INTEGER PRIMARY KEY NOT NULL,
    Name TEXT
);
```


## Invoice
```
CREATE TABLE Invoice
(
    InvoiceID INTEGER PRIMARY KEY NOT NULL,
    CustomerID INTEGER NOT NULL,
    InvoiceDate DATE NOT NULL,
    BillingAddress TEXT,
    BillingCity TEXT,
    BillingState TEXT,
    BillingCountry TEXT,
    BillingPostalCode TEXT,
    Total REAL NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customer (CustomerID)
		ON DELETE NO ACTION ON UPDATE NO ACTION
);
```
<!-- .element: style="font-size:95%" -->


## InvoiceLine
```
CREATE TABLE InvoiceLine
(
    InvoiceLineID INTEGER PRIMARY KEY NOT NULL,
    InvoiceID INTEGER NOT NULL,
    TrackID INTEGER NOT NULL,
    UnitPrice REAL NOT NULL,
    Quantity INTEGER NOT NULL,
    FOREIGN KEY (InvoiceID) REFERENCES Invoice (InvoiceID)
		ON DELETE NO ACTION ON UPDATE NO ACTION,
    FOREIGN KEY (TrackID) REFERENCES Track (TrackID)
		ON DELETE NO ACTION ON UPDATE NO ACTION
);
```


## MediaType
```
CREATE TABLE MediaType
(
    MediaTypeID INTEGER PRIMARY KEY NOT NULL,
    Name TEXT
);
```


## PlayList
```
CREATE TABLE Playlist
(
    PlaylistID INTEGER PRIMARY KEY NOT NULL,
    Name TEXT
);
```


## PlayListTrack
```
CREATE TABLE PlaylistTrack
(
    PlaylistID INTEGER NOT NULL,
    TrackID INTEGER NOT NULL,
    PRIMARY KEY (PlaylistID, TrackID),
    FOREIGN KEY (PlaylistID) REFERENCES Playlist (PlaylistID)
		ON DELETE NO ACTION ON UPDATE NO ACTION,
    FOREIGN KEY (TrackID) REFERENCES Track (TrackID)
		ON DELETE NO ACTION ON UPDATE NO ACTION
);
```
<!-- .element: style="font-size:95%" -->


## Track
```
CREATE TABLE Track
(
    TrackID INTEGER PRIMARY KEY NOT NULL,
    Name TEXT NOT NULL,
    AlbumID INTEGER,
    MediaTypeID INTEGER NOT NULL,
    GenreID INTEGER,
    Composer TEXT,
    Millisecond INTEGER NOT NULL,
    Byte INTEGER,
    UnitPrice REAL NOT NULL,
    FOREIGN KEY (AlbumID) REFERENCES Album (AlbumID)
		ON DELETE NO ACTION ON UPDATE NO ACTION,
    FOREIGN KEY (GenreID) REFERENCES Genre (GenreID)
		ON DELETE NO ACTION ON UPDATE NO ACTION,
    FOREIGN KEY (MediaTypeID) REFERENCES MediaType (MediaTypeID)
		ON DELETE NO ACTION ON UPDATE NO ACTION
);
```
<!-- .element: style="font-size:85%" -->



## Q01: Who am I (5%)
- Write a single SELECT statement to project your first name, last name, student ID and a short description of yourself as four string literals. Rename the column headings appropriately


## Sample output
<<<<<<< HEAD
=======

>>>>>>> master
```
First Name  Last Name   ID          Description
----------  ----------  ----------  -------------
Johnny      Chan        9999999     I am the king
```

<<<<<<< HEAD
<br />
- 🎉 unlocked by Nicholas!

=======
>>>>>>> master


## Q02: Who the F (5%)
- Write a single SQL statement to list all the artists that begin their name with the letter F (including both upper and lower cases). The output should include all columns from the Artist table


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
ArtistID    Name
----------  -------------------------------
23          Frank Zappa & Captain Beefheart
39          Fernanda Porto
82          Faith No More
83          Falamansa
84          Foo Fighters
85          Frank Sinatra
86          Funk Como Le Gusta
241         Felix Schmidt, London Symphony
251         Fretwork
```
>>>>>>> master



## Q03: Order by name (5%)
- Write a single SQL statement to list all employee names (each combining the first name and the last name with a space in between) from the Employee table. Sort the output by the length of the employee name, with the longest one to go first in the list


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
Name
----------------
Michael Mitchell
Laura Callahan
Nancy Edwards
Margaret Park
Steve Johnson
Andrew Adams
Jane Peacock
Robert King
```
>>>>>>> master



## Q04: Fix the fax (5%)
- You are told that one employee has a fax number stored with a missing + sign at the front, but you do not know which employee has done that. All other employees have their fax numbers starting with the + sign

- Write a single SQL statement (without using subquery) to update that particular fax number by adding a + sign at the front of it


## Sample output
- yet to be unlocked!


## Q05: Create the country (8%)
- Write a single SQL statement to create a new table named Country with four columns: CountryID (Integer), Name (Text), Desc (Text) and Code (Text)

  - Assign CountryID as the primary key of the table
  - The Name of a country should never be NULL
  - Set the default value of Desc to 'A Happy Place'
  - Define a check on Code to make sure they are always less than or equal to seven characters long


## No sample output



## Q06: Find the right song (8%)
- Write a single SQL statement to list all the tracks that have the exact word 'right' (including both upper and lower cases) as part of the name in the Track table. In other words, it will not include track names with words like 'rights' or 'righteous' in the output


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
Name
--------------------------------------------------
Right Through You
Night Time Is The Right Time
You Can't Do it Right (With the One You Love)
Right Next Door to Hell
Always Be All Right
Get Right
Right On Time
The Right Thing
Right Now
You Got No Right
I Guess You're Right
```
>>>>>>> master



## Q07: Album luxury (8%)
- Write a single SQL statement to list albums with three columns: the title of the album, the total number of tracks in that album, and the price of the album. Exclude albums that are priced lower than thirty dollars from the output. Rename the column headings appropriately, and sort the output by the price descendingly


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
Album                                               Tracks      Price
--------------------------------------------------  ----------  ----------
Greatest Hits                                       57          56.43
Lost, Season 3                                      26          51.74
Lost, Season 1                                      25          49.75
The Office, Season 3                                25          49.75
Battlestar Galactica (Classic), Season 1            24          47.76
Lost, Season 2                                      24          47.76
Heroes, Season 1                                    23          45.77
The Office, Season 2                                22          43.78
Battlestar Galactica, Season 3                      19          37.81
LOST, Season 4                                      17          33.83
Minha Historia                                      34          33.66
```
<!-- .element: style="font-size:85%" -->
>>>>>>> master



## Q08: Youngest manager (8%)
- Write a single SQL statement to show the first name and the age of an employee who is the youngest manager in the company. The age should be shown as a whole number (i.e. without any decimal places) in the output


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
Name                  Age
--------------------  ----------
Michael               43
```
>>>>>>> master



## Q09: Quick music (8%)
- Write a single SQL statement to create a new playlist called 'Quick Music'; and write another single SQL statement to associate the new playlist with the 10 shortest duration tracks from the Track table


## Sample output
- yet to be unlocked!



## Q10: AAC (8%)
- Write a single SQL statement to generate two rows of information: one row showing the number of tracks formatted in AAC media type, and the other row showing the number of tracks formatted in non-AAC media type. There should be two columns in the output: first column is named Media which has the value AAC or non-AAC; second column is named Tracks which shows the total number of tracks


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
Media                 Tracks
--------------------  ----------
AAC                   255
non-AAC               3248
```
>>>>>>> master



## Q11: Multi genre (8%)
- Write a single SQL statement to project two columns for a list: the title of an album in the first column, and the names of genre that the album is associated with in the second column. Exclude albums that associate with only one genre, and rename the column headings appropriately


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
Album                 Genre
--------------------  -----------------------------------------
Battlestar Galactica  TV Shows,Science Fiction,Sci Fi & Fantasy
Greatest Hits         Rock,Reggae,Metal
Heroes, Season 1      TV Shows,Drama
LOST, Season 4        Drama,TV Shows
Live After Death      Heavy Metal,Metal
Lost, Season 2        TV Shows,Drama
Lost, Season 3        TV Shows,Drama
Rock In Rio CD2       Rock,Metal
The Number of The Be  Metal,Rock
The Office, Season 3  TV Shows,Comedy
Unplugged             Blues,Latin
```
<!-- .element: style="font-size:90%" -->
>>>>>>> master



## Q12: Email provider (8%)

- Write a single SQL statement to generate a list with two columns: Provider and Percentage
  - The first column displays email provider in upper cases (e.g. GMAIL, YAHOO), and the information could be obtained from the email of customer. Email from the same provider with different country code (e.g. yahoo.com, yahoo.de, yahoo.ca) should be considered as part of the same email provider (e.g. YAHOO)
  - The second column displays the percentage of customer with two decimal places
  - Sort the output first by Percentage descendingly, then by Provider ascendingly


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
Provider    Percentage
----------  ----------
YAHOO       30.51     
GMAIL       13.56     
APPLE       11.86     
HOTMAIL     6.78      
SHAW        5.08      
AOL         3.39      
SURFEU      3.39      
UOL         3.39      
COMCAST     1.69      
EMBRAER     1.69      
GOOGLE      1.69      
JETBRAINS   1.69      
JUBII       1.69      
MICROSOFT   1.69      
REDIFF      1.69      
RIOTUR      1.69      
ROGERS      1.69      
SAPO        1.69      
WOODSTOCK   1.69      
WP          1.69      
YACHOO      1.69      
```
<!-- .element: style="font-size:65%" -->
>>>>>>> master



## Q13: View the customer (8%)

- Write a single SQL statement to create a view named CustomerView. The view should have three columns: Country, Individual and Company
  - The first column includes all the countries found in the Customer table
  - The second column and the third column display the number of individual and company customers in each country respectively
  - Both second and third columns display only whole number
  - A company customer is defined by the presence of value in the column Company of the Customer table; an individual customer is defined by the absence of value in that same column
  - Sort the output by country ascendingly
  - You are told that you cannot use OUTER JOIN for this particular task


## Sample output
<<<<<<< HEAD
- yet to be unlocked!
=======
```
SELECT * FROM CustomerView;

Country               Individual  Company
--------------------  ----------  ----------
Argentina             1           0
Australia             1           0
Austria               1           0
Belgium               1           0
Brazil                1           4
Canada                6           2
Chile                 1           0
Czech Republic        1           1
Denmark               1           0
Finland               1           0
France                5           0
Germany               4           0
Hungary               1           0
India                 2           0
Ireland               1           0
Italy                 1           0
Netherlands           1           0
Norway                1           0
Poland                1           0
Portugal              2           0
Spain                 1           0
Sweden                1           0
USA                   10          3
United Kingdom        3           0
```
<!-- .element: style="font-size:55%" -->
>>>>>>> master



## Q14: We are so lost (8%)

- Write a single SQL statement to create a trigger named UndeleteLostTrack. The objective of this trigger is to cancel the effect of deleting any track from the Track table that associates with LOST the TV show (which could be referenced from the title of an album)
  - The trigger does not stop the deletion; but it cancels its effect by recreating the exact same row or rows of deleted track or tracks
  - The trigger ignores deletion of track that has no association with LOST


## Sample output
- yet to be unlocked!



# THE END
<canvas width=300 height=300 class="anything">
<!--
{
  "initialize": "function(container) {
	var width = container.width,
	    height = container.height;
	var projection = d3.geo.orthographic()
	    .translate([width / 2, height / 2])
	    .scale(width / 2 - 20)
	    .clipAngle(90)
	    .precision(0.6);

	var c = container.getContext('2d');

	var path = d3.geo.path()
	    .projection(projection)
	    .context(c);

	var title = container.parentElement.querySelector('.country');
	queue()
	    .defer(d3.json, '../asset/world-110m.json')
	    .defer(d3.tsv, '../asset/world-country-names.tsv')
	    .await(ready);

	function ready(error, world, names) {
	  if (error) throw error;

	  var globe = {type: 'Sphere'},
	      land = topojson.feature(world, world.objects.land),
	      countries = topojson.feature(world, world.objects.countries).features,
	      borders = topojson.mesh(world, world.objects.countries, function(a, b) { return a !== b; }),
	      i = -1,
	      n = countries.length;

	  countries = countries.filter(function(d) {
	    return names.some(function(n) {
	      if (d.id == n.id) return d.name = n.name;
	    });
	  }).sort(function(a, b) {
	    return a.name.localeCompare(b.name);
	  });

	  (function transition() {
	    d3.transition()
	        .duration(1250)
	        .each('start', function() {
			while ( !countries[i = (i + 1) % n] ) {};			
			title.innerHTML = (countries[i].name);
	        })
	        .tween('rotate', function() {
	          var p = d3.geo.centroid(countries[i]),
	              r = d3.interpolate(projection.rotate(), [-p[0], -p[1]]);
	          return function(t) {
	            projection.rotate(r(t));
	            c.clearRect(0, 0, width, height);
	            c.fillStyle = '#fff', c.lineWidth = 2, c.beginPath(), path(globe), c.fill();
	            c.fillStyle = '#42affa', c.beginPath(), path(land), c.fill();
	            c.fillStyle = '#f00', c.beginPath(), path(countries[i]), c.fill();
	            c.strokeStyle = '#ccc', c.lineWidth = .5, c.beginPath(), path(borders), c.stroke();
	            c.strokeStyle = '#ccc', c.lineWidth = 2, c.beginPath(), path(globe), c.stroke();
	          };
	        })
	      .transition()
	        .each('end', transition);
	  })();
	}

	d3.select(self.frameElement).style('height', height + 'px');

    }"
}
-->
</canvas>

#### Chinook rules in <span class="country">Everywhere</span>!
[<i class="fa fa-print"></i>](?print-pdf#)
