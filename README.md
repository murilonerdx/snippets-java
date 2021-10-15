
-------------------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#quicksort)Quicksort

``` {.highlight}
  public static void quickSort(int[] arr, int left, int right) {
    var pivotIndex = left + (right - left) / 2;
    var pivotValue = arr[pivotIndex];
    var i = left;
    var j = right;
    while (i <= j) {
      while (arr[i] < pivotValue) {
        i++;
      }
      while (arr[j] > pivotValue) {
        j--;
      }
      if (i <= j) {
        var tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
        i++;
        j--;
      }
      if (left < i) {
        quickSort(arr, left, j);
      }
      if (right > i) {
        quickSort(arr, i, right);
      }
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#bubblesort)Bubblesort

``` {.highlight}
  public static void bubbleSort(int[] arr) {
    var lastIndex = arr.length - 1;

    for(var j = 0; j < lastIndex; j++) {
      for(var i = 0; i < lastIndex - j; i++) {
        if(arr[i] > arr[i + 1]) {
          var tmp = arr[i];
          arr[i] = arr[i + 1];
          arr[i + 1] = tmp;
        }
      }
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#selectionsort)Selectionsort

``` {.highlight}
  public static void selectionSort(int[] arr) {
    var len = arr.length;
        
    for (var i = 0; i < len - 1; i++) {
      var minIndex = i;
        
      for (var j = i + 1; j < len; j++) {
        if(arr[j] < arr[minIndex])
          minIndex = j;
      }
        
      var tmp = arr[minIndex];
      arr[minIndex] = arr[i];
      arr[i] = tmp;
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#insertionsort)InsertionSort

``` {.highlight}
  public static void insertionSort(int[] arr) {
    for (var i = 1; i < arr.length; i++) {
      var tmp = arr[i];
      var j = i - 1;

      while (j >= 0 && arr[j] > tmp) {
        arr[j + 1] = arr[j];
        j--;
      }
      arr[j + 1] = tmp;
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#countingsort)CountingSort

``` {.highlight}
  public static void countingSort(int[] arr) {
    var max = Arrays.stream(arr).max().getAsInt();

    var count = new int[max + 1];

    for (var num : arr) {
      count[num]++;
    }

    for (var i = 1; i <= max; i++) {
      count[i] += count[i - 1];
    }

    var sorted = new int[arr.length];
    for (var i = arr.length - 1; i >= 0; i--) {
      var cur = arr[i];
      sorted[count[cur] - 1] = cur;
      count[cur]--;
    }

    var index = 0;
    for (var num : sorted) {
      arr[index++] = num;
    }
  }
```

[**](https://java-design-patterns.com/snippets.html#array-1)Array
-----------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#generic-two-array-concatenation)Generic two array concatenation

``` {.highlight}
  public static <T> T[] arrayConcat(T[] first, T[] second) {
    var result = Arrays.copyOf(first, first.length + second.length);
    System.arraycopy(second, 0, result, first.length, second.length);
    return result;
  }
```

### [**](https://java-design-patterns.com/snippets.html#generic-n-array-concatenation)Generic N array concatenation

``` {.highlight}
  public static <T> T[] nArrayConcat(T[] first, T[]... rest) {
    var totalLength = first.length;
    for (var array : rest) {
      totalLength += array.length;
    }
    var result = Arrays.copyOf(first, totalLength);
    var offset = first.length;
    for (var array : rest) {
      System.arraycopy(array, 0, result, offset, array.length);
      offset += array.length;
    }
    return result;
  }
```

### [**](https://java-design-patterns.com/snippets.html#check-if-all-elements-of-array-are-equal)Check if all elements of array are equal

``` {.highlight}
  public static <T> boolean allEqual(T[] arr) {
    return Arrays.stream(arr).distinct().count() == 1;
  }
```

### [**](https://java-design-patterns.com/snippets.html#find-maximum-integer-from-the-array)Find maximum integer from the array

``` {.highlight}
  public static int findMax(int[] arr) {
    return Arrays.stream(arr).reduce(Integer.MIN_VALUE, Integer::max);
  }
```

[**](https://java-design-patterns.com/snippets.html#encoding-1)Encoding
-----------------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#base64-encode-string)Base64 encode string

``` {.highlight}
  public static String encodeBase64(String input) {
    return Base64.getEncoder().encodeToString(input.getBytes());
  }
```

### [**](https://java-design-patterns.com/snippets.html#base64-decode-string)Base64 decode string

``` {.highlight}
  public static String decodeBase64(String input) {
    return new String(Base64.getDecoder().decode(input.getBytes()));
  }
```

[**](https://java-design-patterns.com/snippets.html#file-1)File
---------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#list-directories)List directories

``` {.highlight}
  public static File[] listDirectories(String path) {
    return new File(path).listFiles(File::isDirectory);
  }
```

### [**](https://java-design-patterns.com/snippets.html#list-files-in-directory)List files in directory

``` {.highlight}
  public static File[] listFilesInDirectory(final File folder) {
    return folder.listFiles(File::isFile);
  }
```

### [**](https://java-design-patterns.com/snippets.html#list-files-in-directory-recursively)List files in directory recursively

``` {.highlight}
  public static List<File> listAllFiles(String path) {
    var all = new ArrayList<File>();
    var list = new File(path).listFiles();

    if (list != null) {  // In case of access error, list is null
      for (var f : list) {
        if (f.isDirectory()) {
          all.addAll(listAllFiles(f.getAbsolutePath()));
        } else {
          all.add(f.getAbsoluteFile());
        }
      }
    }
    return all;
  }
```

### [**](https://java-design-patterns.com/snippets.html#read-lines-from-file-to-string-list)Read lines from file to string list

``` {.highlight}
  public static List<String> readLines(String filename) throws IOException {
    return Files.readAllLines(new File(filename).toPath());
  }
```

### [**](https://java-design-patterns.com/snippets.html#zip-file)Zip file

``` {.highlight}
  public static void zipFile(String srcFilename, String zipFilename) throws IOException {
    var srcFile = new File(srcFilename);
    try (
            var fileOut = new FileOutputStream(zipFilename);
            var zipOut = new ZipOutputStream(fileOut);
            var fileIn = new FileInputStream(srcFile);
    ) {
      var zipEntry = new ZipEntry(srcFile.getName());
      zipOut.putNextEntry(zipEntry);
      final var bytes = new byte[1024];
      int length;
      while ((length = fileIn.read(bytes)) >= 0) {
        zipOut.write(bytes, 0, length);
      }
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#zip-multiple-files)Zip multiple files

``` {.highlight}
  public static void zipFiles(String[] srcFilenames, String zipFilename) throws IOException {
    try (
      var fileOut = new FileOutputStream(zipFilename);
      var zipOut = new ZipOutputStream(fileOut);
    ) {
      for (var i=0; i<srcFilenames.length; i++) {
        var srcFile = new File(srcFilenames[i]);
        try (var fileIn = new FileInputStream(srcFile)) {
          var zipEntry = new ZipEntry(srcFile.getName());
          zipOut.putNextEntry(zipEntry);
          final var bytes = new byte[1024];
          int length;
          while ((length = fileIn.read(bytes)) >= 0) {
            zipOut.write(bytes, 0, length);
          }
        }
      }
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#zip-a-directory)Zip a directory

``` {.highlight}
  public static void zipDirectory (String srcDirectoryName, String zipFileName) throws IOException {
    var srcDirectory = new File(srcDirectoryName);
    try (
      var fileOut = new FileOutputStream(zipFileName);
      var zipOut = new ZipOutputStream(fileOut)
    ) {
      zipFile(srcDirectory, srcDirectory.getName(), zipOut);
    }
  }
  public static void zipFile(File fileToZip, String fileName, ZipOutputStream zipOut) 
      throws IOException {
    if (fileToZip.isHidden()) { // Ignore hidden files as standard
      return;
    }
    if (fileToZip.isDirectory()) {
      if (fileName.endsWith("/")) {
        zipOut.putNextEntry(new ZipEntry(fileName)); // To be zipped next
        zipOut.closeEntry();
      } else {
        // Add the "/" mark explicitly to preserve structure while unzipping action is performed
        zipOut.putNextEntry(new ZipEntry(fileName + "/"));
        zipOut.closeEntry();
      }
      var children = fileToZip.listFiles();
      for (var childFile : children) { // Recursively apply function to all children
        zipFile(childFile, fileName + "/" + childFile.getName(), zipOut);
      }
      return;
    }
    try (
        var fis = new FileInputStream(fileToZip) // Start zipping once we know it is a file
    ) {
      var zipEntry = new ZipEntry(fileName);
      zipOut.putNextEntry(zipEntry);
      var bytes = new byte[1024];
      var length = 0;
      while ((length = fis.read(bytes)) >= 0) {
        zipOut.write(bytes, 0, length);
      }
    }
  }
```

[**](https://java-design-patterns.com/snippets.html#math-1)Math
---------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#fibonacci)Fibonacci

``` {.highlight}
  public static int fibonacci(int n) {
    if (n <= 1) {
      return n;
    } else {
      return fibonacci(n - 1) + fibonacci(n - 2);
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#factorial)Factorial

``` {.highlight}
  public static int factorial(int number) {
    var result = 1;
    for (var factor = 2; factor <= number; factor++) {
      result *= factor;
    }
    return result;
  }
```

### [**](https://java-design-patterns.com/snippets.html#haversine-formula)Haversine formula

``` {.highlight}
  // Radius of sphere on which the points are, in this case Earth.
  private static final double SPHERE_RADIUS_IN_KM = 6372.8;

  public static double findHaversineDistance(double latA, double longA, double latB, double longB) {
    if (!isValidLatitude(latA)
        || !isValidLatitude(latB)
        || !isValidLongitude(longA)
        || !isValidLongitude(longB)) {
      throw new IllegalArgumentException();
    }

    // Calculate the latitude and longitude differences
    var latitudeDiff = Math.toRadians(latB - latA);
    var longitudeDiff = Math.toRadians(longB - longA);

    var latitudeA = Math.toRadians(latA);
    var latitudeB = Math.toRadians(latB);

    // Calculating the distance as per haversine formula
    var a = Math.pow(Math.sin(latitudeDiff / 2), 2)
            + Math.pow(Math.sin(longitudeDiff / 2), 2) * Math.cos(latitudeA) * Math.cos(latitudeB);
    var c = 2 * Math.asin(Math.sqrt(a));
    return SPHERE_RADIUS_IN_KM * c;
  }

  // Check for valid latitude value
  private static boolean isValidLatitude(double latitude) {
    return latitude >= -90 && latitude <= 90;
  }

  // Check for valid longitude value
  private static boolean isValidLongitude(double longitude) {
    return longitude >= -180 && longitude <= 180;
  }
```

### [**](https://java-design-patterns.com/snippets.html#lottery)Lottery

``` {.highlight}
  public static Integer[] performLottery(int numNumbers, int numbersToPick) {
    var numbers = new ArrayList<Integer>();
    for(var i = 0; i < numNumbers; i++) {
      numbers.add(i+1);
    }

    Collections.shuffle(numbers);
    return numbers.subList(0, numbersToPick).toArray(new Integer[numbersToPick]);
  }
```

### [**](https://java-design-patterns.com/snippets.html#greatest-common-divisor)Greatest Common Divisor

``` {.highlight}
  public static int gcd(int a, int b) { 
    if (b == 0) 
      return a; 
    return gcd(b, a % b);  
  }
```

### [**](https://java-design-patterns.com/snippets.html#prime)Prime

``` {.highlight}
  public static boolean isPrime(int number) {
    if (number < 3) {
      return true;
    }

    // check if n is a multiple of 2
    if (number % 2 == 0) {
      return false;
    }

    // if not, then just check the odds
    for (var i = 3; i * i <= number; i += 2) {
      if (number % i == 0) {
        return false;
      }
    }
    return true;
  }
```

[**](https://java-design-patterns.com/snippets.html#media-1)Media
-----------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#capture-screen)Capture screen

``` {.highlight}
  public static void captureScreen(String filename) throws AWTException, IOException {
    var screenSize = Toolkit.getDefaultToolkit().getScreenSize();
    var screenRectangle = new Rectangle(screenSize);
    var robot = new Robot();
    var image = robot.createScreenCapture(screenRectangle);
    ImageIO.write(image, "png", new File(filename));
  }
```

[**](https://java-design-patterns.com/snippets.html#networking-1)Networking
---------------------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#http-get)HTTP GET

``` {.highlight}
  public static HttpResponse<String> httpGet(String uri) throws Exception {
    var client = HttpClient.newHttpClient();
    var request = HttpRequest.newBuilder()
            .uri(URI.create(uri))
            .build();
    return client.send(request, BodyHandlers.ofString());
  }
```

### [**](https://java-design-patterns.com/snippets.html#http-post)HTTP POST

``` {.highlight}
  public static HttpResponse<String> httpPost(String address, HashMap<String,String> arguments) 
    throws IOException, InterruptedException {
    var sj = new StringJoiner("&");
    for(var entry : arguments.entrySet()) {
      sj.add(URLEncoder.encode(entry.getKey(), "UTF-8") + "="
              + URLEncoder.encode(entry.getValue(), "UTF-8"));
    }

    var out = sj.toString().getBytes(StandardCharsets.UTF_8);
    var request = HttpRequest.newBuilder()
            .uri(URI.create(address))
            .headers("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8")
            .POST(BodyPublishers.ofByteArray(out))
            .build();

    return HttpClient.newHttpClient().send(request, BodyHandlers.ofString());
  }
```

[**](https://java-design-patterns.com/snippets.html#string-1)String
-------------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#palindrome-check)Palindrome check

``` {.highlight}
  public static boolean isPalindrome(String s) {
    var sb = new StringBuilder();
    for (var c : s.toCharArray()) {
      if (Character.isLetter(c)) {
        sb.append(c);
      }
    }

    var forward = sb.toString().toLowerCase();
    var backward = sb.reverse().toString().toLowerCase();
    return forward.equals(backward);
  }
```

### [**](https://java-design-patterns.com/snippets.html#reverse-string)Reverse string

``` {.highlight}
  public static String reverseString(String s) {
    return new StringBuilder(s).reverse().toString();
  }
```

### [**](https://java-design-patterns.com/snippets.html#string-to-date)String to date

``` {.highlight}
  public static Date stringToDate(String date, String format) throws ParseException {
    var simpleDateFormat = new SimpleDateFormat(format);
    return simpleDateFormat.parse(date);
  }
```

### [**](https://java-design-patterns.com/snippets.html#anagram-check)Anagram Check

``` {.highlight}
  public boolean isAnagram(String s1, String s2) { 
    var l1 = s1.length();
    var l2 = s2.length();
    var arr1 = new int[256];
    var arr2 = new int[256];
    if (l1 != l2) {
      return false;
    }
    
    for (var i = 0; i < l1; i++) {
      arr1[s1.charAt(i)]++;
      arr2[s2.charAt(i)]++;
    }

    return Arrays.equals(arr1, arr2);
  }
```

### [**](https://java-design-patterns.com/snippets.html#find-levenshtein-distance)Find Levenshtein distance

``` {.highlight}
  public static int findLevenshteinDistance(String word1, String word2) {
    // If word2 is empty, removing
    int[][] ans = new int[word1.length() + 1][word2.length() + 1];
    for (int i = 0; i <= word1.length(); i++) {
      ans[i][0] = i;
    }

    // if word1 is empty, adding
    for (int i = 0; i <= word2.length(); i++) {
      ans[0][i] = i;
    }

    // None is empty
    for (int i = 1; i <= word1.length(); i++) {
      for (int j = 1; j <= word2.length(); j++) {
        int min = Math.min(Math.min(ans[i][j - 1], ans[i - 1][j]), ans[i - 1][j - 1]);
        ans[i][j] = word1.charAt(i - 1) == word2.charAt(j - 1) ? ans[i - 1][j - 1] : min + 1;
      }
    }
    return ans[word1.length()][word2.length()];
  }
```

### [**](https://java-design-patterns.com/snippets.html#compare-version)Compare Version

``` {.highlight}
  public static int compareVersion(String v1, String v2) {
    Function<String, String[]> getVersionComponents = version -> version.replaceAll(".*?((?<!\\w)\\d+([.-]\\d+)*).*", "$1", "$1").split("\\.");

    var components1 = getVersionComponents.apply(v1);
    var components2 = getVersionComponents.apply(v2);
    int length = Math.max(components1.length, components2.length);

    for (int i = 0; i < length; i++) {
      Integer c1 = i < components1.length ? Integer.parseInt(components1[i]) : 0;
      Integer c2 = i < components2.length ? Integer.parseInt(components2[i]) : 0;
      int result = c1.compareTo(c2);
      if (result != 0) {
        return result;
      }
    }
    return 0;
  }
```

[**](https://java-design-patterns.com/snippets.html#class-1)Class
-----------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#get-methods-name)Get methods name

``` {.highlight}
  public static List<String> getAllMethods(final Class<?> cls) {
    return Arrays.stream(cls.getDeclaredMethods())
            .map(Method::getName)
            .collect(Collectors.toList());
  }
```

### [**](https://java-design-patterns.com/snippets.html#get-public-field-names)Get public field names

``` {.highlight}
  public static List<String> getAllFieldNames(final Class<?> cls) {
    return Arrays.stream(cls.getFields())
            .map(Field::getName)
            .collect(Collectors.toList());
  }
```

### [**](https://java-design-patterns.com/snippets.html#get-all-field-names)Get all field names

``` {.highlight}
  public static List<String> getAllFieldNames(final Class<?> cls) {
      var fields = new ArrayList<String>();
      var currentCls = cls;
      while (currentCls != null) {
        fields.addAll(
            Arrays.stream(currentCls.getDeclaredFields())
                .filter(field -> !field.isSynthetic())
                .map(Field::getName)
                .collect(Collectors.toList()));
        currentCls = currentCls.getSuperclass();
      }
      return fields;
    }
```

### [**](https://java-design-patterns.com/snippets.html#create-object)Create object

``` {.highlight}
  public static Object createObject(String cls)
            throws NoSuchMethodException,
            IllegalAccessException,
            InvocationTargetException,
            InstantiationException,
            ClassNotFoundException {
    var objectClass = Class.forName(cls);
    var objectConstructor = objectClass.getConstructor();
    return objectConstructor.newInstance();
  }
```

[**](https://java-design-patterns.com/snippets.html#io-1)I/O
------------------------------------------------------------

### [**](https://java-design-patterns.com/snippets.html#read-file-by-stream)Read file by stream

``` {.highlight}
  public static List<String> readFile(String fileName) throws FileNotFoundException {
    try (Stream<String> stream = new BufferedReader(new FileReader(fileName)).lines()) {
      return stream.collect(Collectors.toList());
    }
  }
```

### [**](https://java-design-patterns.com/snippets.html#inputstream-to-string)InputStream to String

``` {.highlight}
  public static String inputStreamToString(InputStream inputStream) throws IOException {
    try (var reader = new BufferedReader(new InputStreamReader(inputStream))) {
      var stringBuilder = new StringBuilder();
      var data = reader.read();
 
      while (data != -1) {
        stringBuilder.append((char) data);
        data = reader.read();
      }
      return stringBuilder.toString();
    }
  }
```
