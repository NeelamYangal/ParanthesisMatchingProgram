using System;
using System.Collections.Generic;

namespace Program
{
    public class ParanthesisMatch
    {
        private readonly Dictionary<char, char> _matchingParanthesisCollection =
          new Dictionary<char, char>
          {
            { ')', '('},
            { '}', '{'},
            { ']', '['}
          };

        public bool IsMatched(String expression)
        {
            Stack<char> characterStack = new Stack<char>();
            char c;

            for (int i = 0; i < expression.Length; i++)
            {
                c = expression[i];

                if (c == '(' || c == '{' || c == '[')
                    characterStack.Push(c);
                else if (c == ')' || c == '}' || c == ']')
                {
                    if (characterStack.Count == 0 || (characterStack.Peek() != _matchingParanthesisCollection[c]))
                        return false;
                    else if (characterStack.Peek() == _matchingParanthesisCollection[c])
                        characterStack.Pop();
                }
            }

            return (characterStack.Count == 0);
        }
    }

    class IsParanthesisMatchProgram
    {
        static void Main(string[] args)
        {
            ParanthesisMatch paranthesisMatch = new ParanthesisMatch();

            do
            {
                Console.WriteLine("Please enter expression... Or Press Escape to exit... ");

                string expression = Console.ReadLine();

                Console.WriteLine("Given expression's paranthesis are {0}", paranthesisMatch.IsMatched(expression) ? " Matched" : " not Matched");

            } while (Console.ReadKey().Key != ConsoleKey.Escape);
        }
    }
}
