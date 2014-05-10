---
layout: post
title: "Java Automatic Resource Management"
date: 2013-09-13 13:00
comments: true
categories: [java]
---

You might have seen
[this example](http://docs.oracle.com/javase/tutorial/essential/io/bytestreams.html)
from [The Java Tutorials](http://docs.oracle.com/javase/tutorial/index.html).

{% codeblock lang:java %}
    public class CopyBytes {
        public static void main(String[] args) throws IOException {

            FileInputStream in = null;
            FileOutputStream out = null;

            try {
                in = new FileInputStream("xanadu.txt");
                out = new FileOutputStream("outagain.txt");
                int c;

                while ((c = in.read()) != -1) {
                    out.write(c);
                }
            } finally {
                if (in != null) {
                    in.close();
                }
                if (out != null) {
                    out.close();
                }
            }
        }
    }
{% endcodeblock %}

Unfortunately, this code has a bug. If an exception is thrown while closing
the input stream on line #21, the output stream will not be closed on line #24.

Prior to Java 7 a clean version of this could be written
with the [Commons IO](http://commons.apache.org/proper/commons-io/): IOUtils or
[Google Guava](https://code.google.com/p/guava-libraries/): Closer utility classes.

The following is a correct implementation using [Google Guava](https://code.google.com/p/guava-libraries/).

{% codeblock lang:java %}
    public class CopyBytes {
        public static void main(String[] args) throws IOException {

            Closer closer = Closer.create();

            try {
                InputStream in = closer.register(new FileInputStream("xanadu.txt"));
                OutputStream out = closer.register(new FileOutputStream("outagain.txt"));

                int c;

                while ((c = in.read()) != -1) {
                    out.write(c);
                }
            } catch (Throwable e) {
              throw closer.rethrow(e);
            } finally {
              closer.close();
            }
        }
    }
{% endcodeblock %}

Language support for managing the common pattern makes it even easier in Java 7.

{% codeblock lang:java %}
    public class CopyBytes {
        public static void main(String[] args) throws IOException {
            try (
              FileInputStream in = new FileInputStream("xanadu.txt");
              FileOutputStream out = new FileOutputStream("outagain.txt");

            ) {
                int c;

                while ((c = in.read()) != -1) {
                    out.write(c);
                }
            }
        }
    }
{% endcodeblock %}

Get the details in this [article](http://www.oracle.com/technetwork/articles/java/trywithresources-401775.html)
