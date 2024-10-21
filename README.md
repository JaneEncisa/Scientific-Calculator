# Scientific-Calculator
A simple Scientific Calculator  built using C# that support basic arithmetic operations and scientific operations

namespace Scientific_Calculator
{
    // Service Layer (Application Logic) - Calculation logic included
    public class CalculatorService
    {
        public double Evaluate(string expression)
        {
            // Basic parsing logic (improve for real-world use)
            string[] parts = expression.Split(' ');
            if (parts.Length == 3)
            {
                double a = double.Parse(parts[0]);
                double b = double.Parse(parts[2]);
                string op = parts[1];

                switch (op)
                {
                    case "+": return a + b;
                    case "-": return a - b;
                    case "*": return a * b;
                    case "/":
                        if (b == 0)
                        {
                            throw new DivideByZeroException("Cannot divide by zero.");
                        }
                        return a / b;
                    case "^": return Math.Pow(a, b);
                    default: throw new ArgumentException("Invalid operator.");
                }
            }
            else if (parts.Length == 2)
            {
                double a = double.Parse(parts[1]);
                string op = parts[0];

                switch (op)
                {
                    case "sqrt":
                        if (a < 0)
                        {
                            throw new ArgumentException("Cannot calculate square root of a negative number.");
                        }
                        return Math.Sqrt(a);
                    case "sin": return Math.Sin(a);
                    case "cos": return Math.Cos(a);
                    case "tan": return Math.Tan(a);
                    default: throw new ArgumentException("Invalid operator.");
                }
            }
            else
            {
                throw new ArgumentException("Invalid expression.");
            }
        }
    }

    // Presentation Layer (User Interface)
    internal class Program
    {
        public static void Main(string[] args)
        {
            CalculatorService service = new CalculatorService();

            Console.WriteLine("Scientific Calculator");
            Console.WriteLine("---------------------");
            Console.WriteLine("Supported operations: ");
            Console.WriteLine("Addition (+): ");
            Console.WriteLine("Subtraction (-): ");
            Console.WriteLine("Multiplication (*): ");
            Console.WriteLine("Division (/): ");
            Console.WriteLine("Exponentiation (^): ");
            Console.WriteLine("Square Root (): ");
            Console.WriteLine("Logarithm (log): ");
            Console.WriteLine("Sine (sin): ");
            Console.WriteLine("Cosine (cos): ");
            Console.WriteLine("Tangent (tan): ");
            Console.WriteLine("Exit: ");
            Console.WriteLine("---------------------");

            while (true)
            {
                Console.Write("Enter an expression (or 'exit' to quit): ");
                string input = Console.ReadLine();

                if (input.ToLower() == "exit")
                {
                    break;
                }

                try
                {
                    double result = service.Evaluate(input);
                    Console.WriteLine($"Result: {result}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error: {ex.Message}");
                }
            }
        }
    }
}
