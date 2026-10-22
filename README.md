# Gwent

A two-player desktop version of Gwent, the card game from *The Witcher 3*, built in Java with JavaFX.

Developed for Programming Paradigms (TB025) at the Faculty of Engineering, University of Buenos Aires (FIUBA), first semester of 2025.

## Gameplay

- Two players share the same computer. A coin toss decides who starts.
- Each player has a deck of 21 cards (15 units and 6 special cards) and draws 10 of them.
- Units are placed in one of three rows: close combat, ranged or siege. The player with the most strength on the board wins the round, and the first player to win two rounds wins the match.
- Unit abilities: Agile, Spy, Medic, Tight Bond, Morale Boost and Legendary.
- Special cards: weather (Biting Frost, Torrential Rain, Skellige Storm), Clear Weather, Scorch and Commander's Horn.

## Design

- **MVC:** the game model is independent of the JavaFX views and controllers. An [ArchUnit](https://www.archunit.org/) test enforces this.
- **Game phases** (setup, preparation, play, end) are separate classes that hand control to the next phase.
- **Polymorphism** for cards, abilities, rows and weather instead of type checks.
- **Factory** classes build cards and abilities from the JSON deck definition.
- **Null Object** classes (`CartaNula`, `SinClima`, `SinModificador`) replace `null` checks.
- Unit tests with JUnit 5 and Mockito. UML class and sequence diagrams are in [`diagrams/`](diagrams/).

## Requirements

- Java 11 or later
- [Maven](https://maven.apache.org/)

JavaFX is downloaded by Maven.

## Usage

Run the commands from the repository root.

```bash
mvn clean javafx:run   # run the game
mvn clean test         # run the tests
```

To build a standalone JAR:

```bash
mvn clean package -DskipTests -Ppackage
java -jar target/tp2-0.0.1.jar
```

The decks are read from `src/main/java/edu/fiuba/algo3/archivos/gwent.json`, so the JAR also needs to run from the repository root.

A Docker setup is available in [`docker/`](docker/) (see [`docs/Docker.md`](docs/Docker.md)).

## Project structure

```
src/main/java/edu/fiuba/algo3/
├── modelo/          # game model: cards, abilities, rows, players, rounds, phases
├── vistas/          # JavaFX views
├── controllers/     # controllers between views and model
└── archivos/        # deck definitions (gwent.json)
src/main/test/       # unit and architecture tests
diagrams/            # PlantUML diagrams
```
