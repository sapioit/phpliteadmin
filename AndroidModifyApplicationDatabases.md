This tutorial is to describe how to setup phpliteadmin on your phone running PAW server and a special bash script that modifies application permissions.

Currently I use phpliteadmin to manage all of the database that exist on my rooted Droid X. As an Android developer it is extremely frustrating to have to pull and push your databases off your phone and put them back on your phone whenever you are wanting to make a database change. With phpliteadmin I now don't have to do this. While I am still waiting for multiple bugs to be worked out I believe this is a solid solution for Android developers to manage their development databases and get them ready for production.

If you are un-experienced with Android development the process for creating a database for an application is one of the most frustrating things to deal with and to MANAGE. Your only hope really is to use the Eclipse debugger to make sure your code is executing properly on the database. If you run into a problem or need to change the schema of your database it is almost dauntingly impossible to perform this task inside of the extremely slow debugging life cycle, developers you understand my frustration here. Your only widely available solution is to use something like SQLite Browser and pull the database off your phone and push it back, this just isn't fluent. Below I have posted a process that I currently use for managing my dev and production databases for Android development using phpliteadmin and a few other applications to make the magic happen.

There are a few steps to accomplishing this task. You need two applications and your phone MUST be rooted.
> - PAW Server (PAW Server is an amazing web server for Android)

> - GScript Lite (Executes bash scripts with root access)

You must first install PAW Server from the Android market. Once you have done that you need to install the PHP Plugin for PAW. You can find that by navigating to the URL of your newly installed PAW Server(Your Device) and go to Plugins->PHP Setup.

After you install PAW and the PHP Plugin verify that its working by adding your phpliteadmin.php file to your /app/ folder on your mobile device. If you can navigate to the file and hit it, then you should be good to proceed.

Next install GScript Lite. I have also attached my GScript file that I use to make the magic happen. Take EXTREME caution with proceeding to the next step. If you mess this up or don't perform some type of test before hand to make sure the logic of the code will work for your phone DO NOT PROCEED. I would also encourage you to make a backup of your mobile device before you even execute this script and be in a situation to flash your phone if something messes up.

Download DB Perm and put it on your SD card and load it into GScript. This script file looks at your /data/data/ directory and applies the appropriate permissions to it, so that phpliteadmin can scan the directory structure. In GScript you must give the script file ROOT access so that it can perform this operation. Once the script is done executing go back to your browser and navigate to your phpliteadmin file and you should be able to access every single database for every application that is on your phone.

If you start getting a ton of force closes showing up on your phone then you have messed up, and for some reason the logic of the DB Perm file did not work correctly (although 99% of the time it should work almost all Android devices have the same directory structure at the root level). This is the worst case scenario. Again make a backup before your proceed of your mobile device.

The attached phpliteadmin file is version 1.8.7 I am getting ready to play with 1.8.8 in a moment. Good luck and I hope this works for anyone that tries it. I can help answer any questions :).


Please Note: You must apply the DB Perm file often. The reason, is because of Androids behavior with security and protecting the applications. Every time you open an application, it re-applies the permissions to the application. So if you are working on a database you manage for an app and then open that app up on the phone to test or something. More than likely you will need to re-apply the DB Perm file.

db perm - http://www.mobilemeanbunny.com/blog/phpliteadmin---mobile-management/DBPerm.sh?attredirects=0&d=1

phpliteadmin - http://www.mobilemeanbunny.com/blog/phpliteadmin---mobile-management/phpliteadmin.php?attredirects=0&d=1

Also, if you are looking for just the phpliteadmin code to load all the databases I have posted it below, in case you dont want to wait on me to upload something.

Modify the existing sections appropriately:
```
Previous Versions - 1.8.6 and maybe earlier versions
```
```
$directory = "/data/data";
```
```
//if the user wants to scan a directory for databases, do so
if($directory!==false) {
     if($directory[strlen($directory)-1]=="/") //if user has a trailing slash in the directory, remove it
	$directory = substr($directory, 0, strlen($directory)-1);
		
	if(is_dir($directory)) //make sure the directory is valid 
        {
	     $applications = scandir($directory);
	     $j = 0;
	     foreach ($applications as &$application){
		if ($application != "." && $application != ".."){
		     if(is_dir($directory."/".$application."/databases")) {
			if (is_readable($directory."/".$application."/databases")){
			     $dbdir = scandir($directory."/".$application."/databases");
			     foreach ($dbdir as &$database){
				$file = pathinfo($directory."/".$application."/databases/".$database);
				if(isset($file['extension'])) {
				     $ext = strtolower($file['extension']);
				     if($ext=="sqlite" || $ext=="db" || $ext=="sqlite3" || $ext=="db3") {
					$databases[$j]['path'] = $directory."/".$application."/databases/".$database;
					$databases[$j]['name'] = $application." - ".$database;
					$j++;
				     }
				}else{
				     $databases[$j]['path'] = $directory."/".$application."/databases/".$database;
				     $databases[$j]['name'] = $application." - ".$database;
				     $j++;
				}	
			     }
			}
		     }
		}
	}
	// 22 August 2011: gkf fixed bug #50.
	sort($databases);
     } else { 
     //the directory is not valid - display error and exit
		echo "<div class='confirm' style='margin:20px;'>";
		echo "The directory you specified to scan for databases does not exist or is not a directory.";
		echo "</div>";
		exit();
     }
}
```


```
Version 1.8.9
```
```
$directory = "/data/data";
```
```
//if the user wants to scan a directory for databases, do so
if($directory!==false)
{
     if($directory[strlen($directory)-1]=="/") //if user has a trailing slash in the directory, remove it
          $directory = substr($directory, 0, strlen($directory)-1);
          if(is_dir($directory)) //make sure the directory is valid
          {
	       $applications = scandir($directory);		
	       $j = 0;
	       foreach ($applications as &$application){
	            if ($application != "." && $application != ".."){
		         if(is_dir($directory."/".$application."/databases")) {
			      if (is_readable($directory."/".$application."/databases")){
			           $dbdir = scandir($directory."/".$application."/databases");
				   foreach ($dbdir as &$database){
				        $file = pathinfo($directory."/".$application."/databases/".$database);
					// 22 August 2011: gkf fixed bug 49.
					$perms = 0;
                      
					if(isset($file['extension'])) {
					     $ext = strtolower($file['extension']);
					     if($ext=="sqlite" || $ext=="db" || $ext=="sqlite3" || $ext=="db3") {
                                                  $databases[$j]['path'] = $directory."/".$application."/databases/".$database;
						  $databases[$j]['name'] = $application." - ".$database;
									
						  $perms += is_readable($databases[$j]['path']) ? 4 : 0;
						  $perms += is_writeable($databases[$j]['path']) ? 2 : 0;
						  switch($perms)
						  {
						       case 6: $perms = "[rw] "; break;
						       case 4: $perms = "[r ] "; break;
						       case 2: $perms = "[ w] "; break; // God forbid, but it might happen.
						       default: $perms = "[  ] "; break;
					          }
						  $databases[$j]['perms'] = $perms;
						  $j++;
					     }
				        }else{
					     $databases[$j]['path'] = $directory."/".$application."/databases/".$database;
					     $databases[$j]['name'] = $application." - ".$database;
								
					     $perms += is_readable($databases[$j]['path']) ? 4 : 0;
					     $perms += is_writeable($databases[$j]['path']) ? 2 : 0;
					     switch($perms)
					     {
					     	case 6: $perms = "[rw] "; break;
					     	case 4: $perms = "[r ] "; break;
					      	case 2: $perms = "[ w] "; break; // God forbid, but it might happen.
			                        default: $perms = "[  ] "; break;
				             }
					     $databases[$j]['perms'] = $perms;
					     $j++;
					}	
				   }
			      }  
			 }
		    }
	       }
	       // 22 August 2011: gkf fixed bug #50.
	       sort($databases);
	       if(isset($tdata))
	       {
	            for($i=0; $i<sizeof($databases); $i++)
                    {
	                 if($tdata['path'] == $databases[$i]['path'])
		         {
		              $_SESSION[COOKIENAME.'currentDB'] = $i;
	                      break;
	                 }
	            }
	       }
		
	       if(isset($justrenamed))
	       {
	            for($i=0; $i<sizeof($databases); $i++)
	            {
		         if($newpath == $databases[$i]['path'])
			 {
			      $_SESSION[COOKIENAME.'currentDB'] = $i;
			      break;
			 }
	            }	
	       }
	}
	else //the directory is not valid - display error and exit
	{
		echo "<div class='confirm' style='margin:20px;'>";
		echo "The directory you specified to scan for databases does not exist or is not a directory.";
		echo "</div>";
		exit();
	}
}
```
```
Version 1.9.1
```
```
//if the user wants to scan a directory for databases, do so
if($directory!==false)
{
	if($directory[strlen($directory)-1]=="/") //if user has a trailing slash in the directory, remove it
		$directory = substr($directory, 0, strlen($directory)-1);
		
	if(is_dir($directory)) //make sure the directory is valid
	{
		$applications = scandir($directory);		
		$j = 0;
		foreach ($applications as &$application){
			if ($application != "." && $application != ".."){
				if(is_dir($directory."/".$application."/databases")) {
					if (is_readable($directory."/".$application."/databases")){
						$dbdir = scandir($directory."/".$application."/databases");
						foreach ($dbdir as &$database){
							$file = pathinfo($directory."/".$application."/databases/".$database);
							// 22 August 2011: gkf fixed bug 49.
							$perms = 0;

							if(isset($file['extension'])) {
								$ext = strtolower($file['extension']);
								if($ext=="sqlite" || $ext=="db" || $ext=="sqlite3" || $ext=="db3") {
									//$databases[$j]['perms'] = $perms;
									$databases[$j]['path'] = $directory."/".$application."/databases/".$database;
									$databases[$j]['name'] = $application." - ".$database;
									
									$perms += is_readable($databases[$j]['path']) ? 4 : 0;
									$perms += is_writeable($databases[$j]['path']) ? 2 : 0;
									switch($perms)
									{
										case 6: $perms = "[rw] "; break;
										case 4: $perms = "[r ] "; break;
										case 2: $perms = "[ w] "; break; // God forbid, but it might happen.
										default: $perms = "[  ] "; break;
									}
									$databases[$j]['perms'] = $perms;
									$j++;
								}
							}else{
								$databases[$j]['path'] = $directory."/".$application."/databases/".$database;
								$databases[$j]['name'] = $application." - ".$database;
								
								$perms += is_readable($databases[$j]['path']) ? 4 : 0;
								$perms += is_writeable($databases[$j]['path']) ? 2 : 0;
								switch($perms)
								{
									case 6: $perms = "[rw] "; break;
									case 4: $perms = "[r ] "; break;
									case 2: $perms = "[ w] "; break; // God forbid, but it might happen.
									default: $perms = "[  ] "; break;
								}
								$databases[$j]['perms'] = $perms;
								$j++;
							}	
						}
					}
				}
			}
		}
		// 22 August 2011: gkf fixed bug #50.
		sort($databases);
		if(isset($tdata))
		{
			for($i=0; $i<sizeof($databases); $i++)
			{
				if($tdata['path'] == $databases[$i]['path'])
				{
					$_SESSION[COOKIENAME.'currentDB'] = $i;
					break;
				}
			}
		}
		
		if(isset($justrenamed))
		{
			for($i=0; $i<sizeof($databases); $i++)
			{
				if($newpath == $databases[$i]['path'])
				{
					$_SESSION[COOKIENAME.'currentDB'] = $i;
					break;
				}
			}	
		}
	}
	else //the directory is not valid - display error and exit
	{
		echo "<div class='confirm' style='margin:20px;'>";
		echo "The directory you specified to scan for databases does not exist or is not a directory.";
		echo "</div>";
		exit();
	}
}
```




That is all that really needs to be changed. If you change these sections in the script file they should be good. Leave everything else as is.