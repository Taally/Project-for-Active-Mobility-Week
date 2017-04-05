## Рейсы
Информация о рейсе заполняется пользователем. Описание, дата рейса, дата выписки чека, сумма выплаты, а также ставится отметка о получении выплаты и её дате. 
Вся введённая пользователем информация, а именно: 
```C++
class Truck
{
	tm * _truck_day;	// дата рейса
	tm * _account_day;	// дата выписки счёта
	tm * _fee_day;		// дата получения выплаты
	double _fee;		// размер выплаты
	bool _got_fee;		// наличие выплаты
	string _descr;		// описание рейса (адрес)
	. . . 
};

```

хранятся в векторе рейсов: 
```C++
void create_new_truck(vector<Truck*> & v) {
	Truck* t = new Truck;
	t->change_truck();
	v.push_back(t);
}
```
Просматривать информацию о рейсах можно в двух вариациях: 
- кратко обо всех (включает в себя описание рейса и дату): 
```C++
void show_short_truck_info(const vector<Truck*> & v) {
	for (int i = 0; i < v.size(); ++i) {
		cout << i + 1 << ". " << v[i]->_descr << "; ";
		str_date(cout, v[i]->_truck_day);
	}
}
```
- полно о конкретном рейсе  по его номеру (вся заполненная информация):

```C++
void show_full_truck_info(const vector<Truck*> & v) {
	cout << "Введите номер рейса.\nВведите 0, чтобы выйти.\n";
	int ind;
	cin >> ind;
	while (!(0 <= ind || ind <= v.size())) {
		cout << "Wrong number. Try again.\n";
		cin >> ind;
	}
	if (ind != 0)
		v[ind-1]->print();
}

```
Также, уже после сохранения,  можно вносить изменения в информацию о конкретном рейсе. 
```C++
void change_track(const vector<Truck*> & v) {
	cout << "Введите номер рейса, который вы хотите изменить.\nВведите 0, чтобы выйти.\n";
	int ind;
	cin >> ind;
	while (!(0 <= ind || ind <= v.size())) {
		cout << "Неверный номер. Попробуйте ещё раз.\n";
		cin >> ind;
	}
	if (ind != 0)
		v[ind - 1]->change_truck();
}
```


