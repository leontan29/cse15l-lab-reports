# Lab Report 4

## Part 1: Link to our markdown parse repository and the one we reviewed 

Our repo: https://github.com/mBookUCSD/markdown-parse/blob/main/MarkdownParse.java

The one we reviewed: https://github.com/floatboat/markdown-parse/blob/main/MarkdownParse.java

## Part 2: My MarkdownParseTest code: 

> 
    @Test
    public void testSnip1() throws IOException, NoSuchFileException {

        ArrayList<String> correctOutput = new ArrayList<>();
        correctOutput.addAll(Arrays.asList("`google.com","google.com","ucsd.edu"));
        Path fileName= Path.of("lab8-snip1.md");
        // read the file contents into a string
	    String contents = Files.readString(fileName);
        // run getLinks on the contents of the file
        ArrayList<String> links = MarkdownParse.getLinks(contents);
        assertEquals(correctOutput,links);
    }
    @Test
    public void testSnip2() throws IOException, NoSuchFileException {

        ArrayList<String> correctOutput = new ArrayList<>();
        correctOutput.addAll(Arrays.asList("a.com(())","example.com"));
        Path fileName= Path.of("lab8-snip2.md");
        // read the file contents into a string
	    String contents = Files.readString(fileName);
        // run getLinks on the contents of the file
        ArrayList<String> links = MarkdownParse.getLinks(contents);
        assertEquals(correctOutput,links);
    }
    @Test
    public void testSnip3() throws IOException, NoSuchFileException {

        ArrayList<String> correctOutput = new ArrayList<>();
        correctOutput.addAll(Arrays.asList("https://ucsd-cse15l-w22.github.io/"));
        Path fileName= Path.of("lab8-snip3.md");
        // read the file contents into a string
	    String contents = Files.readString(fileName);
        // run getLinks on the contents of the file
        ArrayList<String> links = MarkdownParse.getLinks(contents);
        assertEquals(correctOutput,links);
    }

## Part 3: Test failures produced by our groups MarkdownParse File 
> 2) testSnip1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com]>
	at org.junit.Assert.fail(Assert.java:89)
	at org.junit.Assert.failNotEquals(Assert.java:835)
	at org.junit.Assert.assertEquals(Assert.java:120)
	at org.junit.Assert.assertEquals(Assert.java:146)
	at MarkdownParseTest.testSnip1(MarkdownParseTest.java:71)
3) testSnip2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com(()), example.com]> but was:<[a.com, a.com((, example.com]>
	at org.junit.Assert.fail(Assert.java:89)
	at org.junit.Assert.failNotEquals(Assert.java:835)
	at org.junit.Assert.assertEquals(Assert.java:120)
	at org.junit.Assert.assertEquals(Assert.java:146)
	at MarkdownParseTest.testSnip2(MarkdownParseTest.java:84)
4) testSnip3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://ucsd-cse15l-w22.github.io/]> but was:<[]>
	at org.junit.Assert.fail(Assert.java:89)
	at org.junit.Assert.failNotEquals(Assert.java:835)
	at org.junit.Assert.assertEquals(Assert.java:120)
	at org.junit.Assert.assertEquals(Assert.java:146)
	at MarkdownParseTest.testSnip3(MarkdownParseTest.java:97)

## Part 4: Test failures produced the other groups MarkdownParse File 
> MarkdownParseTest.java:17: error: incompatible types: String cannot be converted to String[]
        assertEquals(MarkdownParse.getLinks(contents), expect);
                                            ^
MarkdownParseTest.java:24: error: incompatible types: String cannot be converted to String[]
        assertEquals(MarkdownParse.getLinks(contents), expect);
                                            ^
MarkdownParseTest.java:31: error: incompatible types: String cannot be converted to String[]
        assertEquals(MarkdownParse.getLinks(contents), expect);
                                            ^
MarkdownParseTest.java:38: error: incompatible types: String cannot be converted to String[]
        assertEquals(MarkdownParse.getLinks(contents), expect);
                                            ^
MarkdownParseTest.java:45: error: incompatible types: String cannot be converted to String[]
        assertEquals(MarkdownParse.getLinks(contents), expect);
                                            ^
MarkdownParseTest.java:51: error: incompatible types: String cannot be converted to String[]
        assertEquals(expect, MarkdownParse.getLinks(contents));
                                                    ^
MarkdownParseTest.java:57: error: incompatible types: String cannot be converted to String[]
        assertEquals(MarkdownParse.getLinks(contents), expect);
                                            ^
MarkdownParseTest.java:70: error: incompatible types: String cannot be converted to String[]
        ArrayList<String> links = MarkdownParse.getLinks(contents);
                                                         ^
MarkdownParseTest.java:83: error: incompatible types: String cannot be converted to String[]
        ArrayList<String> links = MarkdownParse.getLinks(contents);
                                                         ^
MarkdownParseTest.java:96: error: incompatible types: String cannot be converted to String[]
        ArrayList<String> links = MarkdownParse.getLinks(contents);

## Part 5: Do you think there is a small code change that will work for snippet 1? 

For our implementation of MarkdownParse, I believe that one code change we could make for cases related to backtiks could be to find a backtick and skip it and the character it is escaping. This change would need to be written in the else statement, before identifying a bracket. 

## Part 6: Do you think there is a small code change that will work for snippet 2? 

I believe that one code change we could make for cases related to nest parentheses, brackets, and escaped brackets could be to pair close and opening parentheses. This change essentially searching for a corresponding parentheses, brackets, and escaped bracket everytime and would be checked after finding a link 

## Part 7: Do you think there is a small code change that will work for snippet 3? 

I do not believe there is a small code change that will fix all related cases that have newlines in brackets and parentheses for snippet 3. Looking at snippet 3, since there are a variety of different parentheses, brackets, and spaces, we would need to completely rewrite our MarkdownParse file 