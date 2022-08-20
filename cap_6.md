Antes de tudo, acho importante declarar que a principal mudança relacionada ao Mockito é que agora é necessário utilizar a anotação @ExtendWith(MockitoExtension.class) na classe de teste. Além disso, os métodos de Mock, Spy, InjectMocks e Captor agora são também anotações. @Mock, @Spy, @InjectMocks e @Captor.

Então, é importante lembrar que toda classe que utiliza o Mockito, deve possuir a anotação @ExtendWith(MockitoExtension.class).

## Página 147-148
### Antigo

```java

TicTacToeCollection collection;
@Before
public void before() throws UnknownHostException {
 collection = new TicTacToeCollection();
}
@Test
public void whenInstantiatedThenMongoHasDbNameTicTacToe() {
// throws UnknownHostException {
// TicTacToeCollection collection = new TicTacToeCollection();
 assertEquals(
  "tic-tac-toe",
  collection.getMongoCollection().getDBCollection().getDB().getName()
 );
}
@Test
public void whenInstantiatedThenMongoHasNameGame() {
// throws UnknownHostException {
// TicTacToeCollection collection = new TicTacToeCollection();
 assertEquals(
  "game",
  collection.getMongoCollection().getName());
}

```

### Novo

```java

TicTacToeCollection collection;
@BeforeEach
public void beforeEach() throws UnknownHostException {
 collection = new TicTacToeCollection();
}
@Test
public void whenInstantiatedThenMongoHasDbNameTicTacToe() {
// throws UnknownHostException {
// TicTacToeCollection collection = new TicTacToeCollection();
 assertEquals(
  "tic-tac-toe",
  collection.getMongoCollection().getDBCollection().getDB().getName()
 );
}
@Test
public void whenInstantiatedThenMongoHasNameGame() {
// throws UnknownHostException {
// TicTacToeCollection collection = new TicTacToeCollection();
 assertEquals(
  "game",
  collection.getMongoCollection().getName());
}


```

------------------------------------------------------------
 
## Página 150
### Antigo

```java

import static org.mockito.Mockito.*;
...
@Before
public void before() throws UnknownHostException {
 collection = spy(new TicTacToeCollection());
}

```

### Novo

```java


import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
public class TicTacToeTest { 
    // Classe criada com o intuito de demonstrar onde deve ser adicionado o @ExtendWith(MockitoExtension.class).
}
...

@BeforeEach
public void beforeEach() throws UnknownHostException {
 @Spy
 TicTacToeCollection collection = new TicTacToeCollection();
}


```

------------------------------------------------------------
 
## Página 150
### Antigo

```java

@Test
public void whenSaveMoveThenInvokeMongoCollectionSave() {
 TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
 MongoCollection mongoCollection = mock(MongoCollection.class);
 doReturn(mongoCollection).when(collection).getMongoCollection();
 collection.saveMove(bean);
 verify(mongoCollection, times(1)).save(bean);
}

```

### Novo

```java
@Test
public void whenSaveMoveThenInvokeMongoCollectionSave() {
 TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
 MongoCollection mongoCollection = mock(MongoCollection.class);
 Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();
 collection.saveMove(bean);
 Mockito.verify(mongoCollection, times(1)).save(bean);
}


```

------------------------------------------------------------
 
## Página 151
### Antigo

```java

MongoCollection mongoCollection = mock(MongoCollection.class);

doReturn(mongoCollection).when(collection).getMongoCollection();

collection.saveMove(bean);

verify(mongoCollection, times(1)).save(bean);
```

### Novo

```java

MongoCollection mongoCollection = Mockito.mock(MongoCollection.class);

Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();

collection.saveMove(bean);

Mockito.verify(mongoCollection, times(1)).save(bean);

```

------------------------------------------------------------
 
## Página 153
### Antigo

```java

@Test
public void whenSaveMoveThenReturnTrue() {
 TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
 MongoCollection mongoCollection = mock(MongoCollection.class);
 doReturn(mongoCollection).when(collection).getMongoCollection();
 assertTrue(collection.saveMove(bean));
}

```

### Novo

```java

@Test
public void whenSaveMoveThenReturnTrue() {
 TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
 MongoCollection mongoCollection = Mockito.mock(MongoCollection.class);
 Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();
 assertTrue(collection.saveMove(bean));
}

```

------------------------------------------------------------
 
## Página 153-154
### Antigo

```java

TicTacToeCollection collection;
TicTacToeBean bean;
MongoCollection mongoCollection;

@Before
public void before() throws UnknownHostException {
 collection = spy(new TicTacToeCollection());
 bean = new TicTacToeBean(3, 2, 1, 'Y');
 mongoCollection = mock(MongoCollection.class);
}
...
@Test
public void whenSaveMoveThenInvokeMongoCollectionSave() {
// TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
// MongoCollection mongoCollection = mock(MongoCollection.class);
 doReturn(mongoCollection).when(collection).getMongoCollection();
 collection.saveMove(bean);
 verify(mongoCollection, times(1)).save(bean);
}
@Test
public void whenSaveMoveThenReturnTrue() {
// TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
// MongoCollection mongoCollection = mock(MongoCollection.class);
 doReturn(mongoCollection).when(collection).getMongoCollection();
 assertTrue(collection.saveMove(bean));
}

```

### Novo

```java
TicTacToeCollection collection;
TicTacToeBean bean;
MongoCollection mongoCollection;

@BeforeEach
public void beforeEach() throws UnknownHostException {
 collection = spy(new TicTacToeCollection());
 bean = new TicTacToeBean(3, 2, 1, 'Y');
 mongoCollection = mock(MongoCollection.class);
}
...
@Test
public void whenSaveMoveThenInvokeMongoCollectionSave() {
// TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
// MongoCollection mongoCollection = mock(MongoCollection.class);

 Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();
 collection.saveMove(bean);
 Mockito.verify(mongoCollection, times(1)).save(bean);
}
@Test
public void whenSaveMoveThenReturnTrue() {
// TicTacToeBean bean = new TicTacToeBean(3, 2, 1, 'Y');
// MongoCollection mongoCollection = mock(MongoCollection.class);
 Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();
 assertTrue(collection.saveMove(bean));
}
```

------------------------------------------------------------
 
## Página 154
### Antigo

```java

@Test
public void givenExceptionWhenSaveMoveThenReturnFalse() {
 doThrow(new MongoException("Bla"))
 .when(mongoCollection).save(any(TicTacToeBean.class));
 doReturn(mongoCollection).when(collection).getMongoCollection();
 assertFalse(collection.saveMove(bean));
}

```

### Novo

```java

@Test
public void givenExceptionWhenSaveMoveThenReturnFalse() {
 Mockito.doThrow(new MongoException("Bla")).when(mongoCollection).save(any(TicTacToeBean.class));
 Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();
 assertFalse(collection.saveMove(bean));
}

```

------------------------------------------------------------
 
## Página 155
### Antigo

```java

@Test
public void whenDropThenInvokeMongoCollectionDrop() {
 doReturn(mongoCollection).when(collection).getMongoCollection();
 collection.drop();
 verify(mongoCollection).drop();
}


```

### Novo

```java

@Test
public void whenDropThenInvokeMongoCollectionDrop() {
 Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();
 collection.drop();
 Mockito.verify(mongoCollection).drop();
}

```

------------------------------------------------------------
 
## Página 156
### Antigo

```java

@Test
public void whenDropThenReturnTrue() {
 doReturn(mongoCollection).when(collection).getMongoCollection();
 assertTrue(collection.drop());
}

```

### Novo

```java

@Test
public void whenDropThenReturnTrue() {
 Mockito.doReturn(mongoCollection).when(collection).getMongoCollection();
 assertTrue(collection.drop());
}

```

------------------------------------------------------------
 
## Página 159
### Antigo

```java

private TicTacToeCollection collection;

@Before
public final void before() throws UnknownHostException {
 collection = mock(TicTacToeCollection.class);
// ticTacToe = new TicTacToe();
 ticTacToe = new TicTacToe(collection);
}

```

### Novo

```java

private TicTacToeCollection collection;

@BeforeEach
public final void beforeEach() throws UnknownHostException {
 collection = Mockito.mock(TicTacToeCollection.class);
// ticTacToe = new TicTacToe();
 ticTacToe = new TicTacToe(collection);
}

```

------------------------------------------------------------
 
## Página 159
### Antigo

```java

@Test
public void whenPlayThenSaveMoveIsInvoked() {
 TicTacToeBean move = new TicTacToeBean(1, 1, 3, 'X');
 ticTacToe.play(move.getX(), move.getY());
 verify(collection).saveMove(move);
}

```

### Novo

```java

@Test
public void whenPlayThenSaveMoveIsInvoked() {
 TicTacToeBean move = new TicTacToeBean(1, 1, 3, 'X');
 ticTacToe.play(move.getX(), move.getY());
 Mockito.verify(collection).saveMove(move);
}

```

------------------------------------------------------------
 
## Página 161
### Antigo

```java

@Before
public final void before() throws UnknownHostException {
 collection = mock(TicTacToeCollection.class);
doReturn(true).when(collection).saveMove(any(TicTacToeBean.class));
 ticTacToe = new TicTacToe(collection);
}

```

### Novo

```java

@BeforeEach
public final void beforeEach() throws UnknownHostException {
 collection = Mockito.mock(TicTacToeCollection.class);
doReturn(true).when(collection).saveMove(any(TicTacToeBean.class));
 ticTacToe = new TicTacToe(collection);
}

```

------------------------------------------------------------
 
## Página 161-162
### Antigo

```java

@Test
public void whenPlayAndSaveReturnsFalseThenThrowException() {
 doReturn(false).when(collection).saveMove(any(TicTacToeBean.class));
 TicTacToeBean move = new TicTacToeBean(1, 1, 3, 'X');
 exception.expect(RuntimeException.class);
 ticTacToe.play(move.getX(), move.getY());
}

```

### Novo

```java

@Test
public void whenPlayAndSaveReturnsFalseThenThrowException() {
 Mockito.doReturn(false).when(collection).saveMove(any(TicTacToeBean.class));
 TicTacToeBean move = new TicTacToeBean(1, 1, 3, 'X');
 assertThrows(RuntimeException.class);
 ticTacToe.play(move.getX(), move.getY());
}

```