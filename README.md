# Laboratorinis-3.Vector
Eksperimentinis Vector klasės kūrimas

## Tirtų funkcijų pavyzdžiai

### Vector::push_back 
```cpp
void push_back (const value_type& val);
void push_back (value_type&& val);
```
**Testavimo kodas**
```cpp
int main ()
{
  vector<int> myvector;
  int myint;

  std::cout << "Please enter some integers (enter 0 to end):\n";

  do {
    std::cin >> myint;
    myvector.push_back (myint);
  } while (myint);

  std::cout << "myvector stores " << int(myvector.size()) << " numbers.\n";

  return 0;
}

```
Įvesti skaičiai: 8, 5, 6, 7, 0;

**Rezultatas**
```cpp
myvector stores 5 numbers.
```
---
### Vector::pop_back 
```cpp
void pop_back() {
  if (avail != dat)
    alloc.destroy(--avail);
}
```
**Testavimo kodas**
```cpp
int main ()
{
  vector<int> myvector;
  int sum (0);
  myvector.push_back (100);
  myvector.push_back (200);
  myvector.push_back (300);

  while (!myvector.empty())
  {
    sum+=myvector.back();
    myvector.pop_back();
  }

  std::cout << "The elements of myvector add up to " << sum << '\n';

  return 0;
}

```
**Rezultatas**
```cpp
The elements of myvector add up to 600
```
---
### Vector::shrink_to_fit 
```cpp
void shrink_to_fit(){
  if (limit > avail) 
    limit = avail;
  }
  ```
**Testavimo kodas**
```cpp
int main () {
 vector<int> myvector (100);
  std::cout << "1. capacity of myvector: " << myvector.capacity() << '\n';

  myvector.resize(10);
  std::cout << "2. capacity of myvector: " << myvector.capacity() << '\n';

  myvector.shrink_to_fit();
  std::cout << "3. capacity of myvector: " << myvector.capacity() << '\n';

  return 0;
  }
```
**Rezultatas**
```cpp
1. capacity of myvector: 100
2. capacity of myvector: 100
3. capacity of myvector: 10
```
---
### Vector::assign
```cpp
template <class InputIterator> void assign (InputIterator first, InputIterator last);
void assign (size_type n, const value_type& val);
void assign (std::initializer_list<value_type> il);
```
**Testavimo kodas**
```cpp
int main() {
  vector<int> first;
  vector<int> second;
  vector<int> third;

  first.assign (7,100);             // 7 ints with a value of 100

  vector<int>::iterator it;
  it=first.begin()+1;

  second.assign (it,first.end()-1); // the 5 central values of first

  int myints[] = {1776,7,4};
  third.assign (myints,myints+3);   // assigning from array.

  std::cout << "Size of first: " << int (first.size()) << '\n';
  std::cout << "Size of second: " << int (second.size()) << '\n';
  std::cout << "Size of third: " << int (third.size()) << '\n';
  return 0;
}
```
**Rezultatas**
```cpp
Size of first: 7
Size of second: 5
Size of third: 3
```
---
### Relational operators
```cpp
bool operator== (const vector<T>& other);
bool operator!= (const vector<T>& other);
bool operator < (const vector<T> & other);
bool operator <= (const vector<T> & other);
bool operator > (const vector<T> & other);
bool operator >= (const vector<T> & other);
```
**Testavimo kodas**
```cpp
int main ()
{
vector<int> foo (3,100);   // three ints with a value of 100
vector<int> bar (2,200);   // two ints with a value of 200

  if (foo==bar) std::cout << "foo and bar are equal\n";
  if (foo!=bar) std::cout << "foo and bar are not equal\n";
  if (foo< bar) std::cout << "foo is less than bar\n";
  if (foo> bar) std::cout << "foo is greater than bar\n";
  if (foo<=bar) std::cout << "foo is less than or equal to bar\n";
  if (foo>=bar) std::cout << "foo is greater than or equal to bar\n";

  return 0;
}
```
**Rezultatas**
```cpp
foo and bar are not equal
foo is less than bar
foo is less than or equal to bar
```
---
### Išvados
Visos testuotos funkcijos (testai paimti iš https://cplusplus.com/reference/vector/vector/) išvedė tokius rezultatus, kurie buvo nurodyti minėtame puslapyje, tad galima teigti, jog šis sukurtas Vector konteineris veikia taip pat kaip std::vector.

---
### std::vector ir class vector tuščio vektoriaus užpildymo spartos analizė
|                 | 10 000  | 100 000 | 1 000 000 | 10 000 000 | 100 000 000 |
| :-------------- | :-----: | :-----: | :-------: | :--------: | :---------: |
| **vector**| 0.0002555  | 0.0022638  |  0.0197197  |  0.161009   |  1.225   |
| **std::vector**| 0.0002467 | 0.0016784  | 0.0093046  |  0.130455  | 0.924692   |
  
### Atminties perskirstymai užpildant vektorių 100000000 elementų
Naudojant tiek sukurtą class vector tiek std::vector, atminties perskirstymai įvyko 27 kartus. 
### Spartos analizė naudojant duomenų failą su 10000 studentų įrašų
|**VECTOR**|LAIKAS|
| :-------------- | :-----: |
| DUOMENU NUSKAITYMAS IR APDOROJIMAS| 0.242923  |
|RŪŠIAVIMAS PAGAL PAVARDES | 0.140472  |
|STUDENTU DALINIMAS I DVI GRUPES (VIENAS KONTEINERIS) | 0.018869 |
|SPAUSDINIMAS I FAILA BROLIAI SAUNUOLIAI | 0.278901 |
|SPAUSDINIMAS I FAILA PASIDAVELIAI | 0.788084 |
|VISOS PROGRAMOS VEIKIMO LAIKAS | 1.472209 |

|**STD::VECTOR**|LAIKAS|
| :-------------- | :-----: |
| DUOMENU NUSKAITYMAS IR APDOROJIMAS|0.25763 |
|RŪŠIAVIMAS PAGAL PAVARDES | 0.077868   |
|STUDENTU DALINIMAS I DVI GRUPES (VIENAS KONTEINERIS) | 0.018377 |
|SPAUSDINIMAS I FAILA BROLIAI SAUNUOLIAI | 0.463873 |
|SPAUSDINIMAS I FAILA PASIDAVELIAI |0.321941 |
|VISOS PROGRAMOS VEIKIMO LAIKAS | 1.142702   |


