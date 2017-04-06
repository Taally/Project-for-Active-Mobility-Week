## Расходы
Пользователь заполняет данные о расходах, возможно возникших в ходе рейса. 
Вся информация о расходах

```C++
class Expense
{
	Exp _purpose;	// назначение расхода
	double _amount;	// сумма затрат
	tm * _date;		// дата
	. . . 
};

```
хранится  в векторе:
```C++
void create_new_expense(vector<Expense*> & v) {
	Expense* e = new Expense;
	e->change_expense();
	v.push_back(e);
}
```
А после сохраняется в файл и составляется отчёт. 
```C++
void file_expense_report(const vector<Expense*> & v) 
{ 
time_t t = time(NULL); 
tm * today = localtime(&t); 
string name; 
name = "expense_report" + std::to_string(today->tm_mday) + "_" + std::to_string(today->tm_mon + 1) + "_" + std::to_string(today->tm_year + 1900) + ".txt"; 
ofstream f; 
f.open(name); 
double fuel, rep, fines; 
amount_for_purpose(v, fuel, rep, fines); 
f « "Потрачено на ГСМ: " « fuel « " р.\n"; 
f « "Потрачено на ремонт и детали: " « rep « " р.\n"; 
f « "Потрачено на штрафы: " « fines « " р.\n"; 
f « "Всего потрачено " « fuel+rep+fines « " р. \n"; 
f.close(); 
}
```

Функция, подсчитывающая суммарные расходы по конкретным причинам: 
- ГСМ
- Ремонт и детали
- Штрафы
```C++
void amount_for_purpose(const vector<Expense*> & v, double & fuel, double & rep, double & fines)
{
	fuel = 0;
	rep = 0;
	fines = 0;
	for (int i = 0; i < v.size(); ++i) {
		switch (v[i]->_purpose)
		{
		case FUEL: 
			fuel += v[i]->_amount;
			break;
		case REPAIR:
			rep += v[i]->_amount;
			break;
		case FINES:
			fines += v[i]->_amount;
			break;
		default:
			break;
		}
	}
}
```
А также функция, подсчитывающая суммарные расходы:
```C++
double total_expense(const vector<Expense*> & v)
{
	double res = 0;
	for (int i = 0; i < v.size(); ++i)
		res += v[i]->_amount;
	return res;
}
```
