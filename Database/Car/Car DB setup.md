Technology: Postgre, Docker

**Docker commands:**
```docker
docker run --name pgrs -e POSTGRES_PASSWORD=postgres -p 5432:5432
```

```docker
docker exec -ti pgrs psql -U postgres
```


**Postgre setup:**

- Creating database (then connecting to it via \\c)
```SQL
CREATE DATABASE car;
```

- Creating **cars** table

brand enum creation
```SQL
CREATE TYPE brand_enum AS ENUM ('Volkswagen', 'Skoda', 'Renault');
```

table creation
```SQL
CREATE TABLE cars (
	numberplate VARCHAR(10) PRIMARY KEY,
	brand brand_enum,
	service_begin DATE,
	CONSTRAINT numberplate_format CHECK (numberplate ~* '(?<!.)[A-Z]{3,4}\d{3}(?!.)')
);
```

- Inserting to **cars** table
```SQL
INSERT INTO cars (numberplate, brand, service_begin)
VALUES ('ABC123', 'Volkswagen', CURRENT_DATE);
```

- Changing constraint
```SQL
ALTER TABLE cars DROP CONSTRAINT numberplate_format;

ALTER TABLE cars ADD CONSTRAINT numberplate_format CHECK (numberplate ~* '\b[a-zA-Z]{3,4}\d{3}\b');

ALTER TABLE cars ADD CONSTRAINT numberplate_format CHECK (numberplate ~* '(?<!.)[A-Z]{3,4}\d{3}(?!.)');
```

- Random values
```SQL
INSERT INTO cars (numberplate, brand, service_begin)
VALUES
('ABC123', 'Volkswagen', CURRENT_DATE),
('XYZ789', 'Volkswagen', CURRENT_DATE),
('PQRS456', 'Skoda', CURRENT_DATE),
('LMNO123', 'Skoda', CURRENT_DATE),
('UVWX789', 'Volkswagen', CURRENT_DATE),
('JKL345', 'Volkswagen', CURRENT_DATE),
('MNP456', 'Skoda', CURRENT_DATE),
('DEF789', 'Volkswagen', CURRENT_DATE),
('GHIJ123', 'Volkswagen', CURRENT_DATE),
('VWXY456', 'Skoda', CURRENT_DATE),
('KLMN789', 'Volkswagen', CURRENT_DATE),
('OPQ234', 'Skoda', CURRENT_DATE),
('STU567', 'Volkswagen', CURRENT_DATE),
('HIJK890', 'Skoda', CURRENT_DATE),
('ABC678', 'Volkswagen', CURRENT_DATE),
('XYZ901', 'Skoda', CURRENT_DATE),
('PQRS234', 'Volkswagen', CURRENT_DATE),
('LMNO567', 'Skoda', CURRENT_DATE),
('UVWX890', 'Volkswagen', CURRENT_DATE),
('JKL678', 'Skoda', CURRENT_DATE),
('MNP901', 'Volkswagen', CURRENT_DATE),
('DEF234', 'Skoda', CURRENT_DATE),
('GHI567', 'Volkswagen', CURRENT_DATE),  
('VWXY890', 'Skoda', CURRENT_DATE),  
('KLMN678', 'Volkswagen', CURRENT_DATE),  
('OPQ901', 'Volkswagen', CURRENT_DATE),  
('STU234', 'Skoda', CURRENT_DATE),  
('HIJ567', 'Volkswagen', CURRENT_DATE),  
('ABC890', 'Volkswagen', CURRENT_DATE),  
('XYZ678', 'Skoda', CURRENT_DATE),  
('PQRS901', 'Volkswagen', CURRENT_DATE),  
('LMNO234', 'Volkswagen', CURRENT_DATE),  
('UVWX567', 'Skoda', CURRENT_DATE),  
('JKL890', 'Volkswagen', CURRENT_DATE),  
('MNP678', 'Volkswagen', CURRENT_DATE),  
('DEF901', 'Volkswagen', CURRENT_DATE),  
('GHI234', 'Skoda', CURRENT_DATE),  
('VWXY567', 'Volkswagen', CURRENT_DATE),  
('KLMN890', 'Skoda', CURRENT_DATE),  
('OPQ678', 'Volkswagen', CURRENT_DATE),  
('STU901', 'Volkswagen', CURRENT_DATE),  
('HIJ234', 'Skoda', CURRENT_DATE),  
('ABC567', 'Skoda', CURRENT_DATE),  
('XYZ890', 'Volkswagen', CURRENT_DATE),  
('PQRS678', 'Volkswagen', CURRENT_DATE),  
('LMNO901', 'Skoda', CURRENT_DATE),  
('UVWX234', 'Volkswagen', CURRENT_DATE),  
('JKL567', 'Volkswagen', CURRENT_DATE),  
('MNP890', 'Skoda', CURRENT_DATE),  
('DEF678', 'Volkswagen', CURRENT_DATE),  
('GHI789', 'Volkswagen', CURRENT_DATE),  
('VWXY901', 'Renault', CURRENT_DATE),  
('KLMN234', 'Renault', CURRENT_DATE),  
('OPQ567', 'Renault', CURRENT_DATE),  
('STU890', 'Renault', CURRENT_DATE),  
('HIJ678', 'Renault', CURRENT_DATE);
```

- Checking the number of cars grouped by the length of numberplates
```SQL
SELECT COUNT(numberplate) as "NUMBER OF CARS", LENGTH(numberplate) as "CHARACTERS IN NUMBERPLATE" FROM cars GROUP BY(LENGTH(numberpl
ate));
```