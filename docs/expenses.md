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
void save_expenses(const vector<Expense*> & v)
{
	std::locale::global(std::locale(""));
	ofstream f;
	f.open(create_exp_filename());
	for each(auto e in v) {
		f << expense_to_str(e->_purpose) << ";";
		f << e->_date->tm_mday << ";" << e->_date->tm_mon << ";" << e->_date->tm_year << ";";
		f << e->_amount << ";";
		delete e;
	}
	f.close();
}
```

Есть возможность создать отчёт (вывести на экран), подсчитывающий суммарные расходы по конкретным причинам: 
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
А также суммарные расходы.
```C++
double total_expense(const vector<Expense*> & v)
{
	double res = 0;
	for (int i = 0; i < v.size(); ++i)
		res += v[i]->_amount;
	return res;
}
```
