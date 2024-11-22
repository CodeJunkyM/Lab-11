import java.io.*;

/**
* File: Lab11Prob01.java
* Class: CSCI 1302
* Author: Kilijah Thomas, Jaylen monroe
* Created on: November 22, 2024
* Last Modified: November 22, 2024
* Description:Reads from a binary file (person.dat) and writes its contents to another binary file (people-copy.dat).
*/

public class Lab11Prob01 {
    public static void main(String[] args) {
        // Define file paths
        String inputFilePath = "src/person.dat";
        String outputFilePath = "src/people-copy.dat";

        try (
            // Set up input and output streams
            DataInputStream input = new DataInputStream(new FileInputStream(inputFilePath));
            DataOutputStream output = new DataOutputStream(new FileOutputStream(outputFilePath))
        ) {
            // Infinite loop to read all records until EOF
            while (true) {
                try {
                    // Read data from the binary file
                    int age = input.readInt(); // Read age (int)
                    String firstName = input.readUTF(); // Read first name (UTF-8)
                    String lastName = input.readUTF(); // Read last name (UTF-8)
                    String address = input.readUTF(); // Read address (UTF-8)
                    int zipCode = input.readInt(); // Read zip code (int)
                    double salary = input.readDouble(); // Read salary (double)

                    // Print data to the console
                    System.out.printf("Age: %d, Name: %s %s, Address: %s, Zip: %d, Salary: %.2f%n",
                            age, firstName, lastName, address, zipCode, salary);

                    // Write data to the output file
                    output.writeInt(age);
                    output.writeUTF(firstName);
                    output.writeUTF(lastName);
                    output.writeUTF(address);
                    output.writeInt(zipCode);
                    output.writeDouble(salary);

                } catch (EOFException e) {
                    // End of file reached
                    break;
                }
            }
            System.out.println("Data successfully copied to " + outputFilePath);
        } catch (IOException e) {
            // Handle IO exceptions
            e.printStackTrace();
        }
    }
}
