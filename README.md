# Ambasing
// ZADANIE 1
#include <iostream>
using namespace std;

int main()
{
    int T[] = {1, 3, 2, 3, 4, 1, 5, 6, 2, 3, 4};
    int n = 11;
    int maks_dl = 1;
    int akt_dl = 1;
    int i;

    for (i=1; i<n; i++)
    {
        if (T[i] >= T[i-1])
            akt_dl++;
        else
        {
            if (akt_dl > maks_dl)
                maks_dl = akt_dl;
            akt_dl = 1;
        }
    }

    if (akt_dl > maks_dl)
        maks_dl = akt_dl;

    cout << maks_dl << endl;

    return 0;
}










// ZADANIE 2
#include <iostream>
using namespace std;

int main()
{
    int T[] = {1, -2, 3, 4, -1, 2, 1, -5, 4};
    int n = 9;
    int maks_sum = T[0];
    int akt_sum = T[0];
    int i;

    for (i=1; i<n; i++)
    {
        if (akt_sum + T[i] > T[i])
            akt_sum = akt_sum + T[i];
        else
            akt_sum = T[i];

        if (akt_sum > maks_sum)
            maks_sum = akt_sum;
    }

    cout << maks_sum << endl;

    return 0;
}













// ZADANIE 3
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

void Losuj(int T[], int n)
{
    int i;
    srand(time(0));

    for (i=0; i<n; i++)
        T[i] = rand()%21 - 10;
}

void NajdluzszeRosnace(int T[], int n)
{
    int podciagi[100][100];
    int dl[100];
    int ile = 0;

    int akt[100];
    int a = 0;

    int maks_dl = 1;
    int i, j;

    for (i=0; i<n; i++)
    {
        if (i==0 || T[i] > T[i-1])
            akt[a++] = T[i];
        else
        {
            if (a > maks_dl)
            {
                maks_dl = a;
                ile = 1;

                for (j=0; j<a; j++)
                    podciagi[0][j] = akt[j];

                dl[0] = a;
            }
            else if (a == maks_dl)
            {
                for (j=0; j<a; j++)
                    podciagi[ile][j] = akt[j];

                dl[ile] = a;
                ile++;
            }

            a = 1;
            akt[0] = T[i];
        }
    }

    if (a > maks_dl)
    {
        maks_dl = a;
        ile = 1;
        for (j=0; j<a; j++)
            podciagi[0][j] = akt[j];
        dl[0] = a;
    }
    else if (a == maks_dl)
    {
        for (j=0; j<a; j++)
            podciagi[ile][j] = akt[j];
        dl[ile] = a;
        ile++;
    }

    for (i=0; i<ile; i++)
    {
        for (j=0; j<dl[i]; j++)
            cout << podciagi[i][j] << " ";
        cout << endl;
    }
}

int main()
{
    int n;
    int T[100];
    int i;

    cout << "Podaj liczbe elementow: ";
    cin >> n;

    Losuj(T, n);

    for (i=0; i<n; i++)
        cout << T[i] << " ";
    cout << endl;

    NajdluzszeRosnace(T, n);

    return 0;
}

















// ZADANIE 4
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

void Losuj(int T[], int n)
{
    int i;
    srand(time(0));

    for (i=0; i<n; i++)
        T[i] = rand()%201 - 100;
}

void NajdluzszyDodatni(int T[], int n)
{
    int maks = 0, akt = 0;
    int start = -1, koniec = -1;
    int pocz = 0;
    int i;

    for (i=0; i<n; i++)
    {
        if (T[i] > 0)
        {
            if (akt == 0)
                pocz = i;
            akt++;
        }
        else
        {
            if (akt > maks)
            {
                maks = akt;
                start = pocz;
                koniec = i-1;
            }
            akt = 0;
        }
    }

    if (akt > maks)
    {
        maks = akt;
        start = pocz;
        koniec = n-1;
    }

    if (maks > 0)
    {
        for (i=start; i<=koniec; i++)
            cout << T[i] << " ";
        cout << endl;
    }
    else
        cout << "Brak" << endl;
}

int main()
{
    int n;
    int T[100];
    int i;

    cout << "Podaj liczbe elementow: ";
    cin >> n;

    Losuj(T, n);

    for (i=0; i<n; i++)
        cout << T[i] << " ";
    cout << endl;

    NajdluzszyDodatni(T, n);

    return 0;
}















// ZADANIE 5
#include <iostream>
using namespace std;

void PodciagiSumy(int T[], int n, int suma)
{
    int i, j, k;
    int s;
    bool ok = false;

    for (i=0; i<n; i++)
    {
        s = 0;

        for (j=i; j<n; j++)
        {
            s = s + T[j];

            if (s == suma)
            {
                for (k=i; k<=j; k++)
                    cout << T[k] << " ";
                cout << endl;

                ok = true;
            }
        }
    }

    if (!ok)
        cout << "Brak" << endl;
}

int main()
{
    int n, suma;
    int T[100];
    int i;

    cout << "Podaj liczbe elementow: ";
    cin >> n;

    for (i=0; i<n; i++)
        cin >> T[i];

    cout << "Podaj sume: ";
    cin >> suma;

    PodciagiSumy(T, n, suma);

    return 0;
}
