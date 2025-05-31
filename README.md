# CB Rádió (Középszintű informatika érettségi 2019)

A CB Rádió érettségi feladatsor alapján megoldásra kerül 5 feladat, amelyekkel átismételjük az eddig tanult programozási algoritmusokat.

## Tartalomjegyzék
  ### [1. feladat](#Beolvasás)
  ### [2. feladat](#decideFourBc())
  ### [3. feladat](#nameInput())
  ### [4. feladat](#mostBc())
  ### [5. feladat](#differentDrivers())

## 1. Beolvasás:
  Olvasd be a cb.txt fájlban levő adatokat, és tárold el a további feladatok megoldására alkalmas adatszerkezetben!
  ```c#
   List<Adas> naplo = new List<Adas>();
 StreamReader sr = new StreamReader("cb.txt");
 sr.ReadLine(); 
 string line = string.Empty;

 while ((line = sr.ReadLine())!=null)
 {
     string[] sor = line.Split(';');
     naplo.Add(new Adas(
         int.Parse(sor[0]),
         int.Parse(sor[1]),
         int.Parse(sor[2]),
         sor[3]
     ));
 }
 sr.Close();

  ```

## 2. decideFourBc():
  Döntsd el és írd ki a képernyőre, hogy található-e a naplóban olyan
  bejegyzés, amely szerint a sofőr egy percen belül pontosan 4 adást indított!
  
    ```c#
     public static void decideFourBc(List<Adas> naplo)
    {
    Console.WriteLine("2. feladat:");
    bool talalat = false;
    foreach (Adas adas in naplo)
    {
        if (adas.AdasDb == 4)
        {
            talalat = true;
            break;
        }
    }
        Console.WriteLine(talalat ? "Volt négy adást indító sofőr." : "Nem volt négy adást indító sofőr.");
    }
    ```

## 3. nameInput():
  Kérd be egy sofőr nevét, majd határozd meg a sofőr által indított hívások
  számát a napló bejegyzéseiből! Az eredményt a minta szerint írd ki a képernyőre! Ha olyan
  sofőr nevét adja meg a felhasználó, aki nem szerepel a naplóban, akkor a „Nincs ilyen nevű
  sofőr!” mondat jelenjen meg!

    ```c#
    public static void nameInput(List<Adas> naplo)
    {
        Console.WriteLine("3. feladat:");
        Console.Write("Kérek egy sofőrnevet: ");
        string keresettNev = Console.ReadLine();
        int osszAdas = 0;
        bool vanSofor = false;

    foreach (Adas adas in naplo)
    {
        if (adas.Nev == keresettNev)
        {
            osszAdas += adas.AdasDb;
            vanSofor = true;
        }
        

        if (vanSofor)
        {
            Console.WriteLine($"{keresettNev} {osszAdas}x használta a CB-rádiót.");
        }
        else
        {
            Console.WriteLine("Nincs ilyen nevű sofőr!");
        }
    }
    
    ```

## 4. mostBc():
  Határozd meg a legtöbb adást indító sofőr nevét! A sofőr neve és az általa indított hívások
  száma jelenjen meg a képernyőn!
  
    ```c#
    public static void mostBc(List<Adas> naplo)
    {
        Console.WriteLine("4. feladat:");
        Dictionary<string, int> soforStat = new Dictionary<string, int>();
        foreach (Adas adas in naplo)
        {
            if (soforStat.ContainsKey(adas.Nev)) soforStat[adas.Nev] += adas.AdasDb;
            else soforStat.Add(adas.Nev, adas.AdasDb);
        }

        string legaktivabb = "";
        int maxAdas = 0;
        foreach (var par in soforStat)
        {
            if (par.Value > maxAdas)
            {
                maxAdas = par.Value;
                legaktivabb = par.Key;
            }
        }
        Console.WriteLine($"Legtöbb adást indító sofőr: {legaktivabb}, adások száma: {maxAdas}");
    }
    ```

## 5. differentDrivers():
  Határozd meg és írd ki a képernyőre a sofőrök számát a forrásállományban található
  becenevek alapján! Feltételezheti, hogy nincs két azonos becenév. 

    ```c#
    public static void differentDrivers(List<Adas> naplo)
    {
        Console.WriteLine("5. feladat:");
        List<string> egyediNevek = new List<string>();
    
        foreach (Adas adas in naplo)
        {
            bool marVan = false;
            foreach (string nev in egyediNevek)
            {
                if (nev == adas.Nev)
                {
                    marVan = true;
                    break;
                }
            }
            if (!marVan) egyediNevek.Add(adas.Nev);
        }
        Console.WriteLine($"Sofőrök száma: {egyediNevek.Count} fő");
    }
    ```
  
