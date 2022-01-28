import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.Stack;

public class MarkdownParse {
    public static boolean isEscaped(int currentIndex, String markdown){
        return currentIndex != 0 && markdown.charAt(currentIndex - 1) == '\\';
    }

    public static ArrayList<String> getLinks(String markdown) {
        ArrayList<String> toReturn = new ArrayList<>();
        // find the next [, then find the ], then find the (, then take up to
        // the next )

        int currentIndex = 0;
        while(currentIndex < markdown.length()) {
            int nextOpenBracket = markdown.indexOf("[", currentIndex);
            int nextCloseBracket = markdown.indexOf("]", nextOpenBracket);
            while (isEscaped(nextCloseBracket, markdown)){
                nextCloseBracket = markdown.indexOf("]", nextOpenBracket);
                if (nextCloseBracket == -1) {
                    break;
                }
        Stack<Character> bracketTracker = new Stack<>(); 
        boolean findLink = false;
        int start = 0;
        int end = 0;
        while (currentIndex < markdown.length()) {
            char curr = markdown.charAt(currentIndex);
            //if an escape char is found, skip it and the 
            //character it is escaping
            if (curr == '\\') {
                currentIndex += 2;
                continue;
            }
            int openParen = markdown.indexOf("(", nextCloseBracket);
            int closeParen = markdown.indexOf(")", openParen);
            toReturn.add(markdown.substring(openParen + 1, closeParen));
            currentIndex = closeParen + 1;
            if (markdown.indexOf("[", currentIndex) == -1) {
                currentIndex = markdown.length();
            //if we are potentially looking at a link with []
            if (findLink) {
                // if there arent any other brackets on the bracket tracker
                if (bracketTracker.isEmpty()) {
                    if (curr == '(') {
                        bracketTracker.push(curr);
                        start = currentIndex;
                    } else { //something else came after the ] that wasn't (
                        findLink = false;
                    }
                } else {
                    if (curr == ')') {
                        end = currentIndex;
                        toReturn.add(markdown.substring(start + 1, end));
                        bracketTracker.pop();
                        findLink = false;
                    }
                }
            } else {
                if (curr == '[') {
                    bracketTracker.push(curr);
                } else if (curr == ']') {
                    if (!bracketTracker.isEmpty()) {
                        bracketTracker.clear();
                        findLink = true;
                    }
                } else if (curr == '!') {
                    if (currentIndex < markdown.length() - 1 && markdown.charAt(currentIndex + 1) == '[') {
                        currentIndex += 2;
                    }
                }
            }
            // move to next char
            currentIndex++;
        }

        return toReturn;
    }
    public static void main(String[] args) throws IOException {
        // take in the first command line arg as the file name to be searched for links.
		Path fileName = Path.of(args[0]);
        // read the file contents into a string
	    String contents = Files.readString(fileName);
        // run getLinks on the contents of the file
        ArrayList<String> links = getLinks(contents);
        // print out the links that we found
        System.out.println(links);
    }
} 
