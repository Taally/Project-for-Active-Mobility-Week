## Доходы
Отчёт о доходах формируется на основании архива рейсов. 
```C++
double income(const vector<Truck*> & v)
{
	double res = 0;
	for (int i = 0; i < v.size(); ++i)
		if (v[i]->_got_fee)
		res += v[i]->_fee;
	return res;
}
```
Все отчёты записываются в файлы, которые создаются в каталоге с программой. 
