# LOGARITHMIC_BASE_CONVERTION_100-_ACCURANCY_FINAL_SOULUTION
ALGORITHM FOR BASE CONVERTION 100 % ACCURANCY
ConvertAndReconstruct_by_VIPER&ASSISTANT
Overview
The ConvertAndReconstruct program converts a decimal number to a specified base and then reconstructs the original decimal number from that base. The algorithm splits the number into integer and fractional parts, converts them, and calculates the accuracy of the conversion.

Features
Converts decimal numbers to any specified base (currently supports base 8).
Reverses the conversion to check accuracy.
Calculates the accuracy of the reconstructed number compared to the original number.
Code Explanation
Main Function
csharp

Copy
static void Main()
{
    double number = 457.25;
    int baseToConvert = 8;

    // Convert to base 8
    string base8Result = ConvertToBase(number, baseToConvert);
    Console.WriteLine($"The number {number} in base {baseToConvert} is: {base8Result}");

    // Inverse operation: Convert back to base 10
    double reconstructedNumber = ConvertFromBase(base8Result, baseToConvert);
    Console.WriteLine($"The number {base8Result} in base {baseToConvert} is: {reconstructedNumber}");

    // Calculate accuracy
    double accuracy = Math.Abs(number / reconstructedNumber) * 100;
    Console.WriteLine($"Accuracy of the conversion: {accuracy}%");
}
Purpose: This is the entry point of the program. It initializes a decimal number and the base for conversion.
Conversion: Calls the ConvertToBase method to convert the number to the specified base.
Reconstruction: Calls ConvertFromBase to convert the base representation back to decimal.
Accuracy: Calculates the accuracy of the conversion.
ConvertToBase Method
csharp

Copy
static string ConvertToBase(double number, int baseToConvert)
{
    int integerPart = (int)number;
    double fractionalPart = number - integerPart;

    // Convert the integer part
    string integerBase = ConvertIntegerToBase(integerPart, baseToConvert);

    // Convert the fractional part
    string fractionalBase = ConvertFractionToBase(fractionalPart, baseToConvert);

    return integerBase + fractionalBase;
}
Purpose: Converts a decimal number to the specified base.
Integer and Fractional Parts: Splits the number into its integer and fractional components and converts them separately.
ConvertIntegerToBase Method
csharp

Copy
static string ConvertIntegerToBase(int number, int baseToConvert)
{
    if (number == 0) return "0";

    string result = "";
    while (number > 0)
    {
        int remainder = number % baseToConvert;
        result = remainder.ToString() + result;
        number /= baseToConvert;
    }

    return result;
}
Purpose: Converts the integer part of a number to the specified base.
Conversion Logic: Uses a loop to repeatedly divide the number by the base and build the resulting string.
ConvertFractionToBase Method
csharp

Copy
static string ConvertFractionToBase(double fraction, int baseToConvert)
{
    string result = ".";
    int count = 0;

    while (fraction > 0 && count < 6) // Limit to 6 digits for precision
    {
        fraction *= baseToConvert;
        int integerPart = (int)fraction;
        result += integerPart.ToString();
        fraction -= integerPart;
        count++;
    }

    return result;
}
Purpose: Converts the fractional part of a number to the specified base.
Precision Control: Limits the number of digits to 6 for accuracy.
ConvertFromBase Method
csharp

Copy
static double ConvertFromBase(string baseValue, int baseToConvert)
{
    string[] parts = baseValue.Split('.');
    double integerPart = ConvertIntegerFromBase(parts[0], baseToConvert);
    double fractionalPart = parts.Length > 1 ? ConvertFractionFromBase(parts[1], baseToConvert) : 0;

    return integerPart + fractionalPart;
}
Purpose: Converts a number from a specific base back to decimal.
Splitting: Splits the base representation into integer and fractional parts and calls respective conversion methods.
ConvertIntegerFromBase Method
csharp

Copy
static double ConvertIntegerFromBase(string integerPart, int baseToConvert)
{
    double result = 0;
    for (int i = 0; i < integerPart.Length; i++)
    {
        result = result * baseToConvert + (integerPart[i] - '0');
    }
    return result;
}
Purpose: Converts the integer part from the specified base back to decimal.
Calculation: Iterates through each character and builds the decimal value.
ConvertFractionFromBase Method
csharp

Copy
static double ConvertFractionFromBase(string fractionPart, int baseToConvert)
{
    double result = 0;
    for (int i = 0; i < fractionPart.Length; i++)
    {
        result += (fractionPart[i] - '0') / Math.Pow(baseToConvert, i + 1);
    }
    return result;
}
Purpose: Converts the fractional part from the specified base back to decimal.
Calculation: Uses a loop to compute the decimal value based on the fractional position.
Usage
Clone the repository.
Open the project in a C# IDE.
Run the program to see the conversion and reconstruction in action.
Conclusion
This algorithm provides a straightforward way to convert decimal numbers to a specified base and back, ensuring accuracy through the reconstruction process. Feel free to use, modify, and enhance it for your needs!
