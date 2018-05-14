using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace Matrix
{
    class Program
    {
        static int Height;
        static int Whith; 

        static Random rnd = new Random();

        static object locker = new object();
  
        static void Matrix(object argument)
        {
            Thread.Sleep(rnd.Next(50, 100));
            int stolb = (int)argument;
            int r = rnd.Next(30);  
            int sleep = rnd.Next(5, 10);     
            while (true)
            {
                Thread.Sleep(rnd.Next(10, 50)); 
                lock (locker)
                {
                    if (r < Height)
                    {
                        for (int i = 0; i < r; i++)
                        {
                            Console.ForegroundColor = ConsoleColor.DarkGreen;
                            Console.SetCursorPosition(stolb, i);
                            if (r - i == 1)
                            {
                                Console.ForegroundColor = ConsoleColor.Green;
                                Console.Write("{0}", rnd.Next(0, 2), rnd.Next(0, 2));
                                Console.SetCursorPosition(stolb + 12, i);
                                Thread.Sleep(sleep);
                            }
                            else if (r - i > 1 && r - i < 4)
                            {
                                Console.ForegroundColor = ConsoleColor.White;
                                Console.Write("{0}{1}", rnd.Next(0, 2), rnd.Next(0, 2));
                                Console.SetCursorPosition(stolb + 12, i);
                                Thread.Sleep(sleep);
                            }
                            else
                            {
                                Console.Write("{0}{1}", rnd.Next(0, 2), rnd.Next(0, 2));
                                Console.SetCursorPosition(stolb + 12, i);
                                Console.Write("{0}{1}", rnd.Next(0, 2), rnd.Next(0, 2));
                                Console.SetCursorPosition(stolb + 27, i);
                                Console.Write("{0}{1}", rnd.Next(0, 2), rnd.Next(0, 2));
                                Console.SetCursorPosition(stolb + 39, i);
                                Console.Write("{0}{1}", rnd.Next(0, 2), rnd.Next(0, 2));
                                Thread.Sleep(sleep * 3);
                            }


                        }
                        r += rnd.Next(10, 20);
                        if (r >= Height) r = Height;
                    }
                    else
                    {
                        for (int i = 0; i < r; i++)
                        {
                            Console.SetCursorPosition(stolb, i);
                            Console.Write(" ");
                            Console.SetCursorPosition(stolb + 7, i);
                            Console.Write("{0}", rnd.Next(0, 2));
                            Console.SetCursorPosition(stolb + 27, i);
                            Console.Write(" ");
                            Console.SetCursorPosition(stolb + 39, i);
                            Console.Write(" ");
                        }
                        r = rnd.Next(8, 25);
                    }
                }
            }
        }

        static void Main(string[] args)
        {
            Console.Title = "Matrix";
            Console.SetWindowSize(80, 40);

            Height = Console.WindowHeight;
            Whith = Console.WindowWidth;

            for (int i = 0; i < Console.WindowWidth - 39; i++)
            {
                ParameterizedThreadStart matrix = new ParameterizedThreadStart(Matrix);
                Thread thread = new Thread(matrix);
                thread.Start(i);
            }
        }
    }
}
