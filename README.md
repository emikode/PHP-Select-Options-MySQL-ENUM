# PHP “SELECT” Dropdown menu with MySQL ENUM:

---

> This code snippet written in **PHP**, generates a “**Select**” input type in **HTML**, by taking the allowed values from a **MySQL ENUM** data type.
> 

---

## Code:

```php
<?php

                $HTMLPage= <<<HTML
                    **//INSERT HERE THE HTML CODE YOU ONLY WANT TO SHOW IF THE DROPDOWN MENU HAS BEEN CORRECTLY INSERTED:**
                    <input type="submit" name="submit" value="Submit Form."/>
                    <input type="reset" value="Reset Form" />

                    HTML;

                if($myDBObject = new mysqli("**SERVER_HOSTNAME**","**MySQL_USERNAME**","**MySQL_PASSWORD**")){

                    $myDBObject->select_db("DB_NAME");

                    if(!$queryResult = $myDBObject->query("SHOW COLUMNS FROM **tableName** WHERE Field=\"**columnName**\"")){
		                    echo "<h2>There was an error while creating the page.</h2>";
                    }else{
                        if($queryResult->num_rows == 0){
                            echo "<h2>Check the table definition.";
                        }else{
                            echo"<hr><br><h2>**Title**:</h2>";
                            $enumString = $queryResult->fetch_array()['Type'];
                            $enumString = substr($enumString,6,strlen($enumString)-8);

                            $enumString = str_replace('\'','',$enumString);
                            $arrayEnumOptions = explode(',',$enumString);
                            echo "<select name=\"**select_input_name**\" required>";
                            foreach($arrayEnumOptions as $singleOption){
                                echo "<option value=\"$singleOption\">$singleOption</option>";
                            }
                            echo "</select>";
                            echo $HTMLPage;
                        }
                    }

                }else{
                    echo "<h2>There was an error while creating the page.</h2>";
                }
            ?>
```

---

## Technologies Used

- **PHP**
- **MySQLI**

---

## Usage

Just copy-paste my code snippet in your **.php** file, and modify the highlighted parts according to your needs.

You can insert **HTML** code in the “**$HTMLPage**” variable, to only show that code if the dropdown menu has been correctly generated.

For example, if you don’t want your form to be submittable if the dropdown menu wasn’t generated, insert the submit button code in that part.

---

## Contact

Coded by @emikodes - feel free to contact me!

---
