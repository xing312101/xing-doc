# File IO

### read
```
FileReader fr = new FileReader("FilePath/filename.txt"); BufferedReader br = new BufferedReader(fr);
while (br.ready()) { System.out.println(br.readLine()); }
fr.close();
```
### write
```
FileWriter fw = new FileWriter("filePath/filename.txt"); fw.write("this is test sentence ");
fw.flush();
fw.close();
```

## List File
>  https://stackabuse.com/java-list-files-in-a-directory

### File.list()
```
public class Pathnames {

    public static void main(String[] args) {
        // Creates an array in which we will store the names of files and directories
        String[] pathnames;

        // Creates a new File instance by converting the given pathname string
        // into an abstract pathname
        File f = new File("D:/Programming");

        // Populates the array with names of files and directories
        pathnames = f.list();

        // For each pathname in the pathnames array
        for (String pathname : pathnames) {
            // Print the names of files and directories
            System.out.println(pathname);
        }
    }
}
```

### FilenameFilter
```
File f = new File("D:/Programming");

// This filter will only include files ending with .py
FilenameFilter filter = new FilenameFilter() {
        @Override
        public boolean accept(File f, String name) {
            return name.endsWith(".py");
        }
    };

// This is how to apply the filter
pathnames = f.list(filter);
```


### File.listFiles()
```
public class Pathnames {
    public static void main(String args[]) {

        // try-catch block to handle exceptions
        try {
            File f = new File("D:/Programming");

            FilenameFilter filter = new FilenameFilter() {
                @Override
                public boolean accept(File f, String name) {
                    // We want to find only .c files
                    return name.endsWith(".c");
                }
            };

            // Note that this time we are using a File class as an array,
            // instead of String
            File[] files = f.listFiles(filter);

            // Get the names of the files by using the .getName() method
            for (int i = 0; i < files.length; i++) {
                System.out.println(files[i].getName());
            }
        } catch (Exception e) {
            System.err.println(e.getMessage());
        }
    }
}
```

### Files.walk()
```
public class FilesWalk {
    public static void main(String[] args) {
        try (Stream<Path> walk = Files.walk(Paths.get("D:/Programming"))) {
            // We want to find only regular files
            List<String> result = walk.filter(Files::isRegularFile)
                    .map(x -> x.toString()).collect(Collectors.toList());

            result.forEach(System.out::println);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
