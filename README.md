# POC DynamoDB to MySQL data migration

1. Set AWS credentials on `DynamoDBtoCSV/dynamoDBtoCSV.js`

2. Do the data dump from DynamoDB

    ```console
        $ node DynamoDBtoCSV/dynamoDBtoCSV.js -t homolog-chubaca-carriers > dynamo_output/output.csv
    ```

3. Start Docker services

    ```console
    $ docker-compose up
    ```

4. Enter the container and access database

    ```console
    $ docker-compose exec mysql bash
    $ mysql -u root -p
    ```

5. Create table schema

    ```sql
    CREATE TABLE carrier ...
    ```


6. Run importation command

    ```sql
    LOAD DATA INFILE '/home/dynamo-output/output.csv'
    INTO TABLE table_name
    FIELDS TERMINATED BY ','
    ENCLOSED BY '"'
    LINES TERMINATED BY '/n'
    IGNORE 1 ROWS;
    ```