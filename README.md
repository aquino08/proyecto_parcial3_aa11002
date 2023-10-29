# Parcial3 - Ingeniería de Datos <br>

## Data Set  <br>

Descripción del DataSet de la base de datos transaccional de vuelos <br>

### Tabla: Airlines 

| No.| Nombre      | Tipo de dato | Descripción                                |
|----|-------------|--------------|--------------------------------------------|
| 1  | Code        | String       | Código único identificador de la aerolínea.|
| 1  | Description | String       | Nombre de la aerolínea.    				   |

### Tabla: Flights 

| No.| Nombre      						| Tipo de dato | Descripción                                									|
|----|--------------------------------- |--------------|--------------------------------------------------------------------------------|
| 1  | FlightDate                       | String       | Fecha de vuelo 																|
| 2  | Flight_Number_Operating_Airline  | Integer      | Número de vuelo    															|
| 3  | Origin  						    | String       | Abreviación del aeropuerto de salida       									|
| 4  | OriginCityName  					| String       | Nombre de la ciudad de salida    												|
| 5  | OriginStateName  				| String       | Nombre del estado de salida    												|
| 6  | Dest  							| String       | Abreviación del aeropuerto de llegada    										|
| 7  | DestCityName  					| String       | Nombre de la ciudad de llegada    		    									|
| 8  | DestStateName  					| String       | Nombre del estado de llegada    												|
| 9  | CRSDepTime  						| Integer      | Hora programada de salida    													|
| 10 | DepTime  						| String       | Hora real de salida   				        									|
| 11 | DepDelayMinutes  				| String       | Minutos de retraso en salida  													|
| 12 | CRSArrTime  						| Integer      | Hora programada de llegada   													|
| 13 | ArrTime  						| String       | Hora real de llegada   														|
| 14 | ArrDelayMinutes  				| String       | Minutos de retraso en llegada    												|
| 15 | WheelsOff  						| String       | Hora que el avión se levanta de la tierra (Salida)     						|
| 16 | WheelsOn  						| String       | Hora que el avión toca tierra (Llegada)   										|
| 17 | Cancelled  						| Integer      | Indicador de vuelo cancelado   												|
| 18 | Diverted  						| Integer      | Indicador de vuelo desviado   													|
| 19 | AirTime  						| String       | Tiempo de vuelo en el aire   													|
| 20 | Flights  						| Integer      | Cantidad de vuelos   															|
| 21 | CarrierDelay  				    | String       | Minutos de retraso debido al transportador   									|
| 22 | WeatherDelay  				    | String       | Minutos de retraso debido al clima   											|
| 23 | NASDelay  				        | String       | Minutos de retraso en el Sistema Nacional de Aero espacio 						|
| 24 | SecurityDelay  				    | String       | Minutos de retraso debido a seguridad   										|
| 25 | LateAircraftDelay  				| String       | Minutos de retraso de la aeronave   											|
| 26 | DivReachedDest  				    | String       | Indicador si un vuelo desviado, logró alcanzar su destino inicial programado. 	|


## Diagrama del Dataset

![Diagrama del Data Set](https://github.com/aquino08/proyecto_parcial3_aa11002/blob/main/Imagenes/DataSet_Parcial3_AA11002.png)

## Modelo dimensional

![Modelo Dimensional DW](https://github.com/aquino08/proyecto_parcial3_aa11002/blob/main/Imagenes/ModeloDimensional_Parcial3_AA11002.png)

## S3 y RedShift

Los datos procesados y en formato del Modelo Dimensional son almacenados en el servicio S3 de AWS, para luego ser llevados a la base en Redshift que los contendrá.  <br>

Script utlizado para la creación de la base en Redshift:  <br>

```
CREATE TABLE dimairline(
    AirlineKey int PRIMARY KEY,
    AirlineId Varchar(50) distkey,
    Description Varchar (250)
);

CREATE TABLE dimdate(
    Datekey int PRIMARY KEY distkey,
    fullDate Varchar(10),
    dayName Varchar (15),
	dayOfWeek int,
	dayNumInMonth int,
	monthNumOverall int,
	monthName Varchar (15),
	weekNumInYear int,
	quaterName Varchar (15),
	quater int,
	semesterName Varchar (15),
	semester int,
	year int,
)sortKey(Datekey, monthName, year);

CREATE TABLE factflights(
    AirlineKey int,
    DateKey int distkey,
    Flight_Number_Operating_Airline int,
	Origin Varchar (100),
	OriginCityName Varchar (100),
	OriginStateName Varchar (100),
	Dest Varchar (100),
	DestCityName Varchar (100),
	DestStateName Varchar (100),
	Flights int,
	Airtime int,
	Cancelled Varchar (20),
	Diverted Varchar (20),
	Delayed Varchar (20),
	WheelsOffMinutes Varchar (20),
	WheelsOnMinutes Varchar (20),
	DepDelayMinutes int,
	ArrDelayMinutes int,
	CarrierDelay int,
	WeatherDelay int,
	NASDelay int,
	SecurityDelay int,
	LateAircraftDelay int,
	TotalDelayTime int,
	DivReachedDest Varchar (20),
	FOREIGN KEY(AirlineKey) REFERENCES dimairline(AirlineKey),
	FOREIGN KEY(DateKey) REFERENCES dimdate(Datekey)
)sortKey(AirlineKey, Datekey);

```

## Url de video  <br>

![Url de video de explicación de resolución de parcial 3](https://github.com/aquino08/proyecto_parcial3_aa11002/blob/main/Imagenes/ModeloDimensional_Parcial3_AA11002.png)