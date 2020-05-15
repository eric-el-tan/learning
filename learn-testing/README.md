# learn-testing

## [mockito](https://github.com/mockito/mockito/wiki)

### Good Unit Test 
-	readability = clarity
-	good test method name
-	test should fail only when business logic fail, test should not fail if some other thing breaks
-	test data should relate to test objectives only
-	given/when/then format
```code
@Mock List listMock;
given(listMock.size).willReturn(5);
actual logic;
assertThat(a, is(b));
```
- [FIRST](https://pragprog.com/magazines/2012-01/unit-tests-are-first)
- [Pattern](http://xunitpatterns.com)
- [Mockito - How to write good tests](https://github.com/mockito/mockito/wiki/How-to-write-good-tests) or [Mockito Best Practice](https://stackoverflow.com/questions/22540108/best-practices-with-mockito)
- [in28minutes:Mockito](https://github.com/in28minutes/MockitoTutorialForBeginners/blob/master/Step18.md), [video](https://www.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678796#bookmarks)

### [Real World Mock](https://www.udemy.com/course/mockito-tutorial-with-junit-examples/learn/lecture/5678776#bookmarks) 

- business-impl extends business-api
- business-api composite of data-api, data-impl

### Issue encountered

- PowerMockito
    -   result in ObjenesisException if using higher than Java 8
