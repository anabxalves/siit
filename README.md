# Project Si-It

## I - INITIAL INSTRUCTIONS

***Main.py*** - is the core of the code.

***Auth_functions.py*** - is the code for the login.

***Sql_functions.py*** - is the code for the database.

***Mock_data.py*** - contains mock data for testing purposes of the main code.

***Credits_functions.py*** - contains some graphic elements and the credits.

***Main_database.db*** - is the database.

All of the code listed above was developed on VSCode and can be opened normally as a python archive, all except ***main_databade.db***, that requires extra steps:

1) Install the extension SQLite, on VSCode

2) Press, on your keyboard, the commands *Ctrl+Shift+P* to open the command palette and search and select the tab SQLite: Open Database. 

3) While still in the command palette, select the archive ***main_databade.db***, in which the tab **SQLITE EXPLORER** will appear in the lower part of the VSCode Explorer (*Ctrl+Shift+E*), after which you will use the arrows to navigate the archives.

## II - SUMMARY

The objective of this project is to create a database of tourist attractions, which, when combined, become a travel itinerary. We also implemented the login and personalized itineraries resources, as well as the categorization of the attractions, the saving and export of itineraries, and the creation of random unique combinations. To do so, we utilized not only lists and dictionaries, but also functions, iterations, conditionals, string and archive manipulation, and SQLite to create a simplified database.

## III - LIBRARIES

***Random***
> Generates randomness to create the randomized itinerary, which will be further explained further ahead.

***Time***
> Creates intervals of time during the execution of the code, used for aesthetic purposes, so the exhibition of the code on the terminal can simulate a “search” in the database. It was applied to the random itinerary and the personalized itinerary, which will be detailed further ahead.

***System***
> Through the function system(‘cls’), the terminals’ screen is cleared, to better the aesthetic and clarity of the user interface. Was applied throughout the entire code.

## IV - DATABASE

*SQLite* is a library developed in C language which implements an SQL (*Sequenced Query Language*) relational database, in the form of an archive. Thus, it’s possible to make all the queries to the database and test the program as a whole.

### FUNCTIONS
***connect_to_database()***
> This function is responsible for creating a connection with the SQLite database. It also creates tables of attractions and users, if not already existent. It also returns the connection created.

***create_attractions(connection)***
> This function is responsible for the insertion of data in the table of attractions of the database. It receives the SQLite connection as a parameter, and through the connection can transact the query and insert the attractions into the database.

***create_user(connection, user)***
> This function is responsible for creating a user in the database. It receives the connection and user as parameters, and adds to the table of users the “user”.

***select_attractions(connection)***
> This function is responsible for returning the attractions in the database. It receives the connection as a parameter and searches the attractions in the database throughout the query ‘SELECT’, transforming them into a list of tuples. Then, it transforms the list of tuples into a list of dictionaries and returns a list of users.

***get_attractions(connection)***
> This function is responsible for returning the formatted attractions and receives the connection as a parameter. It receives the attractions from the function select_attractions and formats the schedule of each attraction, transforming a string into a list.

## V - LOGIN

The authentication operates in a way that it’s possible to create a new account and login into the program with a password and passcode generated by the program.

***criar_conta(contas, connection)***
> This function is responsible for creating the user’s account. It receives as parameters a list of accounts and the connection to the database and is responsible for verifying if the user’s CPF already exists in the database. If not existent, the function receives the user’s data through user inputs. Then, it calls the function create_user, transmitting the user’s data and the connection.

***acesso_conta(contas)***
> This function is responsible for logging the user into the program and receives as parameters the list of accounts. It checks if the user’s passcode and password are correct. If correct, returns True and proceeds with the application. If not, returns False and the user can attempt to log in again.

## VI - ATTRACTIONS AND ITINERARIES

The following general structure was defined:

    atraçao={‘ID’: integer identificador ,
        ‘NOME’: ‘Nome da Atração’,
        ‘DESCRICAO’:’descrição da atração’,
        ‘TIPO’:’categoria da atração’,
        'HORARIOS’:’dia/noite,’
        }

>Base-module of the code, with content that forms, in itself, the other lists and dictionaries, a key (ID) to facilitate the manipulation, two keys (‘NOME’ and ‘DESCRICAO’) for exhibition purposes, two keys (‘TIPO’ and ‘HORARIOS’) for filtering and searching. 
> The keys e values are exemplary, there being infinite possibilities of filters

    roteiro={‘ID’: integer identificador ,
        ‘NOME’: ‘Nome do Roteiro’,
        ‘ATRACOES’: [lista de atrações],
            }

> The set of attractions with identifying keys, for exhibition purposes.

    atracoes=[{atracao1}, {atracao2}...]
> List containing all the attractions, to facilitate its search throughout the code.

    roteiros=[{roteiro1}, {roteiro2}, {roteiro3}]]
> List containing all the prepared itineraries, to facilitate the search throughout the code, through iterations.

    meu_roteiro=[{atracao1},{atracao2}... ]
> List of attractions for the user’s personalized itinerary, which has a temporary nature. Is transformed into a dictionary, in the same format as "***roteiro={}***", when saved by the user. 

    meus_roteiros=[{meu_roteiro1}, {meu_roteiro2}...]
> List of personalized itineraries created by the user.

**For better organization, the attractions and the prepared itineraries are located in the archive mock_data.py.**

## VII - MAIN MENU

The main menu is a dictionary, in which the keys are integers and the values are strings. They are printed through a for, being the keys the commands the user must insert to navigate the menu, in which each option calls a subprogram. The number zero (0)  was determined to be the option of exit/return throughout the entire code.

### SUBPROGRAMS

***menu_roteiros()***
> It prints the ID and the NOME of each prepared itinerary and provides the possibility of exporting as a txt archive or returning back to the main menu.

***menu_meu_roteiro()***
> It’s the biggest subprogram of the code, it prints a new menu with four (4) conditions, one of them zero (0), to return, 0 - Voltar:

- Condition 1 calls a new function buscar_passeios(), which has the purpose of filtering and adding the desired attraction to the list meu_roteiro. For such, 3 options are given: display all attractions - which is inside the subprogram -, and the other two options by filtering through type or schedule, which call their respective functions with parameters:
> The functions schedule (time) and type (category) receive the parameter to filter the values of the dictionary of attractions of the list of attractions and request the user if they wish to add the attraction to the list meu_roteiro.
They follow the same concept and can be replicated to whichever filter is needed.

- Condition 2 serves for printing the attractions contained in the list meu_roteiro, if containing itineraries. If not, a timer is activated and the program notifies that there aren’t any itineraries saved. Then, it asks if the user wishes to save the itinerary. If yes, it creates a new dictionary and establishes the itinerary’s ID as the largest ID used in the list meus_roteiros plus one (1), in other words (largest ID)+1=  (new itinerary’s ID). It also asks the user to insert a name for the itinerary, and then adds it to the list meus_roteiros and deletes the list meu_roteiro, so the user can create a new itinerary in the future.

- Condition 3 prints the itineraries saved in the list meus_roteiros through a for, and requests the user to select one of them to view the description of the itinerary. After selecting, it also gives the option to export the itinerary as a txt archive.

The function ***role_aleatorio()*** activates a graphic timer to simulate the processing of the machine, then generates two (2) random numbers, one representing the number of attractions that will be selected and the other to select by the numbers of the attractions in the list atracoes. After that, it asks the user if they wish to save the random itinerary in the list meus_roteiros, so that it can be accessed and exported in the future.

Lastly, the archive credits_functions.py has two functions: ***siit()*** and ***credit()***, which have graphic and aesthetic purposes. They print the brand and the credits of the team, utilizing ASCII art.

## **SIIT**

### **Projeto 1 // CESAR School**

**TEAM:**

Ana Beatriz Alves - abxa@cesar.school

Ana Beatriz Rocha - abrbd@cesar.school

Caio Vila Nova - csvn@cesar.school

Maria Clara Wanderley - mcwa@cesar.school

Edmar Rocha - era@cesar.school

Guilherme Silveira - gsa3@cesar.school

Pedro Coelho - pcdr@cesar.school

Ricardo Lima - rfsl@cesar.school

Sofia Valadares - svc3@cesar.school

Virna Amaral - vfpa@cesar.school

**ADVISERS:**

Geysa Barvalento - gpb2@cesar.org.br

Erick Simões - esm@cesar.school

Rodrigo Larrazábal - rrl@cesar.school
