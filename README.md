public abstract class User
{
    public string FullName { get; set; }
    public DateTime DateOfBirth { get; set; }
    public string Education { get; set; }
    public int WorkExperience { get; set; }
    public string Position { get; set; }
    public string Login { get; set; }
    public string Password { get; set; }

    public abstract void Menu();
}

public class UserManager
{
    private List<User> Users = new List<User>();

    public void AddUser(User user)
    {
        if (Users.Any(u => u.Login == user.Login))
            throw new Exception("Логин уже существует.");
        Users.Add(user);
    }

    public User Authenticate(string login, string password)
    {
        return Users.FirstOrDefault(u => u.Login == login && u.Password == password);
    }

    public void SaveToFile()
    {
        // сериализация списка users в бинарный файл
    }

    public void LoadFromFile()
    {
        // Десериализация списка Users из файла
    }
}

public class program8
{
    public static string GetHiddenPassword()
    {
        string password = "";
        ConsoleKey key;
        do
        {
            var keyInfo = Console.ReadKey(intercept: true);
            key = keyInfo.Key;

            if (key == ConsoleKey.Backspace && password.Length > 0)
            {
                Console.Write("\b \b");
                password = password[..^1];
            }
            else if (!char.IsControl(keyInfo.KeyChar))
            {
                Console.Write("*");
                password += keyInfo.KeyChar;
            }
        } while (key != ConsoleKey.Enter);

        Console.WriteLine();
        return password;
    }
}

public class program6
{
    public void AddEmployee(User user)
    {
        if (DateTime.Now.Year - user.DateOfBirth.Year < 18 ||
            (DateTime.Now.Year - user.DateOfBirth.Year == 18 &&
             DateTime.Now.DayOfYear < user.DateOfBirth.DayOfYear))
        {
            throw new Exception("Сотруднику должно быть минимум 18 лет.");
        }

        // Добавить пользователя в систему
        Console.WriteLine("Сотрудник успешно добавлен.");
    }


}

namespace YourNamespace
{
    public class Item
    {
        public string Name { get; set; }
        public DateTime ExpirationDate { get; set; }
        public double Price { get; set; }
    }

    public class Program
    {
        public static void ApplyDiscount(List<Item> items)
        {
            foreach (var item in items)
            {
                if (item.ExpirationDate < DateTime.Now && item.ExpirationDate > DateTime.Now.AddDays(-14))
                {
                    item.Price *= 0.5;
                }
            }
        }

        public static void Main()
        {
            var items = new List<Item>
            {
                new Item { Name = "молоко", ExpirationDate = DateTime.Now.AddDays(-10), Price = 100 },
                new Item { Name = "сыр", ExpirationDate = DateTime.Now.AddDays(-20), Price = 150 },
                new Item { Name = "хлеб", ExpirationDate = DateTime.Now.AddDays(-5), Price = 50 }
            };

            ApplyDiscount(items);

            foreach (var item in items)
            {
                Console.WriteLine($"{item.Name}: {item.Price}");
            }
        }
    }
}

public class Admin : User
{
    public override void Menu()
    {
        while (true)
        {
            Console.Clear();
            Console.WriteLine("1. Добавить пользователя");
            Console.WriteLine("2. Удалить пользователя");
            Console.WriteLine("3. Просмотр всех данных");
            Console.WriteLine("4. Выйти");

            var key = Console.ReadKey();
            switch (key.Key)
            {
                case ConsoleKey.D1:
                    AddUser();
                    break;
                case ConsoleKey.D2:
                    DeleteUser();
                    break;
                case ConsoleKey.D3:
                    ViewAllData();
                    break;
                case ConsoleKey.D4:
                    return;
            }
        }
    }

    private void AddUser()
    {
        // Реализация добавления пользователя
    }

    private void DeleteUser()
    {
        // Реализация удаления пользователя
    }

    private void ViewAllData()
    {
        // Реализация просмотра всех данных
    }
}
public class taxes
{
    public static double CalculateNetSalary(double grossSalary)
    {
        const double NDFL = 0.13;
        const double PFR = 0.22;
        const double FFOMS = 0.051;
        const double FSS = 0.029;
        const double NS = 0.002;

        double taxes = grossSalary * (NDFL + PFR + FFOMS + FSS + NS);
        return grossSalary - taxes;
    }
}

public class passwordcheck
{
    public static bool IsPasswordValid(string password)
    {
        if (password.Length < 8)
            return false;

        int upperCount = password.Count(char.IsUpper);
        int digitCount = password.Count(char.IsDigit);
        int specialCount = password.Count(c => "!@#$%^&*()".Contains(c));

        return upperCount >= 3 && digitCount >= 3 && specialCount >= 2;
    }
}
