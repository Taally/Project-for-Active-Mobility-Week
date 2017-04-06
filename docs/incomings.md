## Доходы
Отчёт о доходах формируется на основании архива рейсов. 
```C++
string file_income_report(const vector<Expense*> & exp, const vector<Truck*> & trucks) 
{ 
double incm = income(trucks); 
double expn = total_expense(exp); 
time_t t = time(NULL); 
tm * today = localtime(&t); 
string name; 
name = "income_report" + std::to_string(today->tm_mday) + "_" + std::to_string(today->tm_mon + 1) + "_" + std::to_string(today->tm_year+1900) + ".txt"; 
ofstream f; 
f.open(name); 
f « "Выручка: " « incm « " р.\n"; 
f « "Расходы: " « expn « " р.\n"; 
f « "Чистая прибыль: " « incm - expn « " р.\n"; 
f.close(); 
return name; 
}
```
Все отчёты записываются в файлы, которые создаются в каталоге с программой. 
