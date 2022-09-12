## Página 62 - Requirement 1
### Antigo
```java

public class FooTest {
 @Rule
 public ExpectedException exception = ExpectedException.none();
 @Test
 public void whenDoFooThenThrowRuntimeException() {
 Foo foo = new Foo();
 exception.expect(RuntimeException.class);
 foo.doFoo();
 }
}

```
### Novo

```java

public class FooTest {
 @Test
 public void whenDoFooThenThrowRuntimeException() {
 Foo foo = new Foo();
 assertThrows(RuntimeException.class);
 foo.doFoo();
 }
}
```

------------------------------------------------------------
 
## Página 63 - Requirement 1
### Antigo

```java
private Foo foo;
@Before
public final void before() {
 foo = new Foo();
}
```

### Novo

```java
private Foo foo;
@BeforeEach
public final void beforeEach() {
 foo = new Foo();
}
```
------------------------------------------------------------
 
## Página 65 - Board Boundaries 1
### Antigo

```java
package com.packtpublishing.tddjava.ch03tictactoe;
import org.junit.Before;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ExpectedException;
public class TicTacToeSpec {
 @Rule
 public ExpectedException exception = ExpectedException.none();
 private TicTacToe ticTacToe;
 @Before
 public final void before() {
 ticTacToe = new TicTacToe();
 }
 @Test
 public void whenXOutsideBoardThenRuntimeException() {
 exception.expect(RuntimeException.class);
 ticTacToe.play(5, 2);
 }
}

```

### Novo

```java

package com.packtpublishing.tddjava.ch03tictactoe;
import org.junit.Before;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ExpectedException;
public class TicTacToeSpec {

 private TicTacToe ticTacToe;
 @BeforeEach
 public final void beforeEach() {
    ticTacToe = new TicTacToe();
 }
 @Test
 public void whenXOutsideBoardThenRuntimeException() {
    assertThrows(RuntimeException.class);
    ticTacToe.play(5, 2);
 }
}

```

------------------------------------------------------------
 
## Página 66 - Board Boundaries 2
### Antigo

```java

@Test
public void whenYOutsideBoardThenRuntimeException() {
 exception.expect(RuntimeException.class);
 ticTacToe.play(2, 5);
}

```

### Novo

```java

@Test
public void whenYOutsideBoardThenRuntimeException() {
 assertThrows(RuntimeException.class);
 ticTacToe.play(2, 5);
}

```

------------------------------------------------------------
 
## Página 67 - Occupied Spot
### Antigo

```java

@Test
public void whenOccupiedThenRuntimeException() {
 ticTacToe.play(2, 1);
 exception.expect(RuntimeException.class);
 ticTacToe.play(2, 1);
}


```

### Novo

```java

@Test
public void whenOccupiedThenRuntimeException() {
 ticTacToe.play(2, 1);
 assertThrows(RuntimeException.class);
 ticTacToe.play(2, 1);
}

```