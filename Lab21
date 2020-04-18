using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Xml;
using System.Xml.Linq;

namespace lab20
{

    class Bank
    {
        string Number;
        string FIO;
        double AmountAcc;
        DateTime OpenAcc;
        double Perсent;
        public string GetSetNumber
        {
            get
            {
                return Number;
            }
            set // в каждом сете устанавливаем свойства существования объекта
            {
                if (value[0] != '-')
                {
                    if (value.Length == 12)
                    {
                        Number = value;
                    }
                    else
                        throw new Exception("Номер счета должен иметь 12 знаков!");
                }
                else
                    throw new Exception("Номер счета не может быть отрицательным числом!");
            }
        }
        public string GetSetFIO
        {
            get
            {
                return FIO;
            }
            set
            {
                string[] temp = value.Split(' ');
                for (int i = 0; i < temp.Length; i++)
                {
                    string test = temp[i].ToString();
                    if (char.IsLower(test[0]))
                    {
                        throw new Exception("ФИО должно начинаться с большой буквы");
                    }
                }
                FIO = value;
            }
        }
        public double GetSetSum
        {
            get
            {
                return AmountAcc;
            }
            set
            {
                AmountAcc = value;
            }
        }
        public DateTime GetSetDate
        {
            get
            {
                return OpenAcc;
            }
            set
            {
                if (value > new DateTime(1980, 05, 10))
                {
                    OpenAcc = value;
                }
                else
                    throw new Exception("Невозможно открыть счет в банке раньше даты создания банка!");
            }
        }
        public double GetSetPercent
        {
            get
            {
                return Perсent;
            }
            set
            {
                if (value > 0 && value <= 100)
                {
                    Perсent = value;
                }
                else
                    throw new Exception("Процент не может быть отрицательным или привышать 100%");
            }
        }

        public Bank(string number, string FIO, double sum, DateTime date, double perсent) // конструктор с параметрами
        {
            this.Number = number;
            this.FIO = FIO;
            this.AmountAcc = sum;
            this.OpenAcc = date;
            this.Perсent = perсent;
        }
        public void Show() // вывод информации
        {
            Console.WriteLine($"Номер счета: {Number}, ФИО владельца: {FIO}, Баланс: {AmountAcc}$, Дата открытия счета: {OpenAcc.ToString("D")}, Годовой процент начисления: {Perсent}%");
        }
    }

    class Program
    {
        static void MainMenu(List<Bank> acc) // метод мейн меню, создаем свитч, в котором вызываем методы для работы приложения
        {
            Console.Write("1. Вывод текущих данных счетов\n2. Добавить счет\n3. Запросы\n4. Выход\nВаш выбор: ");
            int menu = Convert.ToInt32(Console.ReadLine());
            int temp = 0;
            while (menu > 0 || menu <= 0)
            {
                switch (menu)
                {
                    case 1:
                        OutputXml(acc);
                        //PrintAccounts(acc);
                        temp = 1;
                        break;
                    case 2:
                        AddElementXml();
                        //AddAccount(ref acc);
                        temp = 2;
                        break;
                    case 3:
                        Console.Clear();
                        SubMenu(ref acc);
                        Console.Clear();
                        temp = 3;
                        break;
                    case 4:
                        Console.Write("1. Повторить действие\n2. Выход\nВаш выбор: ");
                        int choice = Convert.ToInt32(Console.ReadLine());
                        if (choice == 1)
                        {
                            if (temp == 1)
                            {
                                goto case 1;
                            }
                            else if (temp == 2)
                            {
                                goto case 2;
                            }
                            else if (temp == 3)
                            {
                                goto case 3;
                            }
                        }
                        else
                        {
                            Console.WriteLine("Выход!");
                            return;
                        }
                        break;
                }
                Console.Write("1. Вывод текущих данных счетов\n2. Добавить счет\n3. Запросы\n4. Выход\nВаш выбор: ");
                menu = Convert.ToInt32(Console.ReadLine());
            }

        }
        static void OutputXml(List<Bank> acc)
        {
            XDocument accounts = new XDocument();
            XElement element = new XElement("Bank");
            foreach (var i in acc)
            {
                XElement temp = new XElement("Account");
                XElement elnumber = new XElement("number", i.GetSetNumber);
                XElement elfio = new XElement("fio", i.GetSetFIO);
                XElement elsum = new XElement("sum", i.GetSetSum);
                XElement eldate = new XElement("date", i.GetSetDate.ToString("D"));
                XElement elperc = new XElement("percent", i.GetSetPercent);
                temp.Add(elnumber);
                temp.Add(elfio);
                temp.Add(elsum);
                temp.Add(eldate);
                temp.Add(elperc);
                element.Add(temp);

            }
            accounts.Add(element);
            accounts.Save("OutputXml.xml");
            Console.WriteLine($"XML-файл успешно сохранён.");
            Console.WriteLine();
            Console.WriteLine("Для возврата в подменю нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static void AddElementXml()
        {
            XmlDocument doc = new XmlDocument();
            doc.Load("OutputXml.xml");
            XmlElement newel = doc.DocumentElement;
            XmlElement account = doc.CreateElement("Account");
            XmlElement accnum = doc.CreateElement("number");
            XmlElement accfio = doc.CreateElement("fio");
            XmlElement accsum = doc.CreateElement("sum");
            XmlElement accdate = doc.CreateElement("date");
            XmlElement accpercent = doc.CreateElement("percent");
            XmlText numtext = doc.CreateTextNode(InitNumber());
            XmlText fiotext = doc.CreateTextNode(InitFIO());
            XmlText sumtext = doc.CreateTextNode(InitSum().ToString());
            XmlText datetext = doc.CreateTextNode(InitDate().ToString("D"));
            XmlText perctext = doc.CreateTextNode(InitPercent().ToString());
            accnum.AppendChild(numtext);
            accfio.AppendChild(fiotext);
            accsum.AppendChild(sumtext);
            accdate.AppendChild(datetext);
            accpercent.AppendChild(perctext);
            account.AppendChild(accnum);
            account.AppendChild(accfio);
            account.AppendChild(accsum);
            account.AppendChild(accdate);
            account.AppendChild(accpercent);
            newel.AppendChild(account);
            doc.Save("OutputXml.xml");
            Console.WriteLine($"объект успешно добавлен в XML-файл.");
            Console.WriteLine();
            Console.WriteLine("Для возврата в подменю нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }

        static void SubMenu(ref List<Bank> acc) // создаем меню запросов, также через свитч, вызывая методы при выборе одного из них
        {
            Console.Write("1. Одновременная сортировка по дате открытия счета и ФИО владельца\n2. Вывод номеров счетов, имеющих одинакового владельца \n3. Вывод ФИО владельцев, открывших свой счет в 2013 году \n4. Вывод максимальной суммы на счете на текущий момент\n5. Группировка по каждому полю\n6. Выход\nВаш выбор: ");
            int submenu = Convert.ToInt32(Console.ReadLine());
            while (submenu > 0 || submenu <= 0)
            {
                switch (submenu)
                {
                    case 1:
                        FristInquiry(ref acc);
                        break;
                    case 2:
                        SecondInquiry(ref acc);
                        break;
                    case 3:
                        ThirdInquiry(ref acc);
                        break;
                    case 4:
                        FourthInquiry(ref acc);
                        break;
                    case 5:
                        FifthInquiry(ref acc);
                        break;
                    case 6:
                        Console.WriteLine("Выход!");
                        return;
                }
                Console.Write("1. Одновременная сортировка по дате открытия счета и ФИО владельца\n2. Вывод номеров счетов, имеющих одинакового владельца \n3. Вывод ФИО владельцев, открывших свой счет в 2013 году \n4. Вывод максимальной суммы на счете на текущий момент\n5. Группировка по каждому полю\n6. Выход\nВаш выбор: ");
                submenu = Convert.ToInt32(Console.ReadLine());
            }
        }
        // ниже методы, которые используются в предыдущих 2-х методах
        static void FristInquiry(ref List<Bank> acc)
        {
            var sortedDateFIO = from i in acc
                                orderby i.GetSetFIO, i.GetSetDate
                                select i;
            foreach (Bank i in sortedDateFIO)
            {
                i.Show();
            }
            Console.WriteLine("Для возврата в подменю нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static void SecondInquiry(ref List<Bank> acc)
        {
            var groupnumber = from i in acc
                              group i by i.GetSetFIO;
            foreach (IGrouping<string, Bank> i in groupnumber)
            {
                Console.WriteLine(i.Key);
                foreach (var j in i)
                {
                    Console.WriteLine(j.GetSetNumber);
                }
            }
            Console.WriteLine("Для возврата в подменю нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static void ThirdInquiry(ref List<Bank> acc)
        {
            var sortFIO = from i in acc
                          where i.GetSetDate.Year == 2013
                          select i;
            int count = 0;
            foreach (Bank i in sortFIO)
            {
                i.Show();
                count++;
            }
            if (count == 0)
                Console.WriteLine("Нет клиентов которые открыли счет в 2013 году");
            Console.WriteLine("Для возврата в подменю нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static void FourthInquiry(ref List<Bank> acc)
        {
            var getsum = from i in acc
                         orderby i.GetSetSum descending
                         select i;
            foreach (Bank i in getsum)
            {
                i.Show();
                break;
            }
            Console.WriteLine("Для возврата в подменю нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static void FifthInquiry(ref List<Bank> acc)
        {
            var groupnumber = from i in acc
                              group i by i.GetSetNumber;
            Console.WriteLine("Группировка по номера счета");
            foreach (IGrouping<string, Bank> i in groupnumber)
            {
                foreach (var j in i)
                {
                    j.Show();
                }
            }

            var groupfio = from i in acc
                           group i by i.GetSetFIO;
            Console.WriteLine("Группировка по ФИО владельца счета");
            foreach (IGrouping<string, Bank> i in groupfio)
            {
                foreach (var j in i)
                {
                    j.Show();
                }
            }

            var groupsum = from i in acc
                           group i by i.GetSetSum;
            Console.WriteLine("Группировка по сумме счета");
            foreach (IGrouping<double, Bank> i in groupsum)
            {
                foreach (var j in i)
                {
                    j.Show();
                }
            }

            var groupdate = from i in acc
                            group i by i.GetSetDate;
            Console.WriteLine("Группировка по дате создания счета");
            foreach (IGrouping<DateTime, Bank> i in groupdate)
            {
                foreach (var j in i)
                {
                    j.Show();
                }
            }

            var groupperc = from i in acc
                            group i by i.GetSetPercent;
            Console.WriteLine("Группировка по годовому проценту начисления");
            foreach (IGrouping<double, Bank> i in groupperc)
            {
                foreach (var j in i)
                {
                    j.Show();
                }
            }
            Console.WriteLine("Для возврата в подменю нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static void PrintAccounts(List<Bank> acc)
        {
            foreach (Bank i in acc)
            {
                i.Show();
            }
            Console.WriteLine("Для возврата в меню нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static void AddAccount(ref List<Bank> acc)
        {
            Console.Write("Введите кол-во счетов сколько хотите добавить: ");
            int count = Convert.ToInt32(Console.ReadLine());
            for (int i = 0; i < count; i++)
            {
                acc.Add(new Bank(InitNumber(), InitFIO(), InitSum(), InitDate(), InitPercent() ));
            }
            Console.WriteLine("Для возврата в меню нажмите любую кнопку!");
            Console.ReadKey();
            Console.Clear();
        }
        static string InitNumber()
        {
            Console.Write("Введите номер счета: ");
            string number = Console.ReadLine();
            return number;
        }
        static string InitFIO()
        {
            Console.Write("Введите ФИО владельца счета: ");
            string fio = Console.ReadLine();
            return fio;
        }
        static double InitSum()
        {
            Console.Write("Введите суммы средств на счету: ");
            double sum = Convert.ToDouble(Console.ReadLine());
            return sum;
        }
        static DateTime InitDate()
        {
            Console.Write("Введите год открытия счета: ");
            int year = Convert.ToInt32(Console.ReadLine());
            Console.Write("Введите месяц открытия счета: ");
            int month = Convert.ToInt32(Console.ReadLine());
            Console.Write("Введите день открытия счета: ");
            int day = Convert.ToInt32(Console.ReadLine());
            return new DateTime(year, month, day);
        }
        static double InitPercent()
        {
            Console.Write("Введите годовой процент начисления: ");
            double percent = Convert.ToDouble(Console.ReadLine());
            return percent;
        }
        static void Main()
        {
            try
            {
                // создаем лист и в него добавляем 10 значений
                List<Bank> accounts = new List<Bank>();
                accounts.Add(new Bank("123456789000", "Выставкин Глеб Сергеевич", 43453, new DateTime(2013, 1, 23), 1));
                accounts.Add(new Bank("483947384231", "Букаткин Владислав Сергеевич", 1243, new DateTime(2012, 5, 25), 2));
                accounts.Add(new Bank("564847631945", "Веракса Леонид Андреевич", 43453, new DateTime(2010, 2, 12), 3));
                accounts.Add(new Bank("124975631954", "Иванов Иван Иванович", 7864, new DateTime(2009, 3, 9), 4));
                accounts.Add(new Bank("234875621456", "Мозоль Алексей Александрович", 4213, new DateTime(2012, 4, 1), 5));
                accounts.Add(new Bank("459756214568", "Макаренко Петр Алексеевич", 35467, new DateTime(2018, 5, 24), 6));
                accounts.Add(new Bank("126749524879", "Юров Юрий Юрьевич", 34574, new DateTime(2019, 6, 10), 7));
                accounts.Add(new Bank("541759426587", "Сабалевский Илья Алексеевич", 45312, new DateTime(2019, 7, 30), 8));
                accounts.Add(new Bank("123457896541", "Лилэкин Артём Петрович", 12345, new DateTime(2012, 8, 10), 9));
                accounts.Add(new Bank("325498542654", "Букашкин Александр Иосифович", 5475, new DateTime(2016, 9, 12), 10));
                MainMenu(accounts);
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
                Console.WriteLine("Нажмите любую кнопку!");
                Console.ReadKey();
                Console.Clear();
                Main();
            }

        }
    }
}
