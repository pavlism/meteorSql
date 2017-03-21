# meteorSql
 A simple meteor example that connects  to a SQL DB
 
 
 # Running
 The project has two run commands, one for a testing system and one for a production system.
 
 Test: meteor run --settings server/TestDBConn.json
 Prod: meteor run --settings server/DBConn.json
 
 The only difference is setting file that is used.  The two files are where you will put you DB connection info. Open up the files and add in yor DB info.
  
File Structure:
 {
    "database": {
      "server"   : "server IP",
      "database" : "DatabaseName",
      "user"     : "User",
      "password" : "Password"
    }
  }
  
  
# SQL
Uses the emgee:mssql package.  The files included will only allow you to run Stored Procedures (that's all I use so I never wrote code to do anything else).  The format to call a SP on you SQL database is this:

var inputs = [{name: "propertyName",type: SQLTypes.NVarChar,value: 'val'}];

Meteor.call('callStoredProcedure', 'SPName', inputs, {}, function (error, result) {
    //do Stuff
});

If the SP doesn't require inputs you can use an empty object.  The other empty object is a placeholder for an output object (something I never used in SQL).  If you don't want to use stored Procedures check out the mrt:reactive-extra for details on how to modify the code.  I do however recommend only using stored procedures for many reasons, but the big one is simple data sanitation.  (https://www.explainxkcd.com/wiki/index.php/327:_Exploits_of_a_Mom)

# Reactivity
Uses the mrt:reactive-extra package.  Thanks the reactivity package we can create reactive arrays.  We can then store results from SQL calls into a reactive array and then have the screen updated (if setup properly).  See the main page for an example.
