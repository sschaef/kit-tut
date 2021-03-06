```java
package edu.kit.list;

import org.junit.Test;

import static org.junit.Assert.*;


public class IntListTest {

    IntList list = new IntList();

    @Test
    public void isEmpty() {
        assertTrue(list.isEmpty());
    }

    @Test
    public void size() {
        assertEquals(0, list.size());
    }

    @Test
    public void add() {
        for (int i = 1; i <= 10; ++i) {
            list.add(i);
        }
        assertEquals(10, list.size());
    }

    @Test(expected = UnsupportedOperationException.class)
    public void getOnEmptyList() {
        list.get(0);
    }

    @Test(expected = UnsupportedOperationException.class)
    public void getOnNegativeValue() {
        list.get(-1);
    }

    @Test(expected = UnsupportedOperationException.class)
    public void getOnValueOutOfRange() {
        for (int i = 1; i <= 10; ++i) {
            list.add(i);
        }
        list.get(10);
    }

    @Test
    public void get() {
        for (int i = 1; i <= 10; ++i) {
            list.add(i);
        }
        assertEquals(1, list.get(0));
        assertEquals(10, list.get(9));
    }

    @Test
    public void mkString() {
        assertEquals("IntList()", list.toString());
        for (int i = 1; i <= 3; ++i) {
            list.add(i);
        }
        assertEquals("IntList(1, 2, 3)", list.toString());

        assertEquals("[1, 2, 3]", list.mkString("[", ", ", "]"));
        assertEquals("123", list.mkString("", "", ""));
    }

    @Test
    public void contains() {
        assertFalse(list.contains(1));
        for (int i = 1; i <= 3; ++i) {
            list.add(i);
        }
        assertTrue(list.contains(1));
        assertTrue(list.contains(3));
        assertFalse(list.contains(4));
        assertFalse(list.contains(-1));
    }

    @Test
    public void of() {
        IntList list = IntList.of(1, 2, 3, 4, 5);
        assertEquals(5, list.size());
        assertEquals("IntList(1, 2, 3, 4, 5)", list.toString());
    }

    @Test(expected = UnsupportedOperationException.class)
    public void nextOnEmptyIterator() {
        IntIterator iter = IntList.of().iterator();
        iter.next();
    }

    @Test
    public void iterator() {
        IntIterator iter = IntList.of(1, 2, 3, 4, 5).iterator();

        assertTrue(iter.hasNext());
        while (iter.hasNext()) {
            int elem = iter.next();
            list.add(elem);
        }
        assertFalse(iter.hasNext());
        
        /*
        // alternative version of iteration
        for (IntIterator it = IntList.of(1, 2, 3, 4, 5).iterator(); it.hasNext();) {
            int elem = it.next();
            list.add(elem);
        }
        */

        assertEquals("IntList(1, 2, 3, 4, 5)", list.toString());
    }
}
```