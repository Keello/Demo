// Ошибок - 14, cтроки => [2,6,14,19,22,28,36,43,47,50,52,58,63,65]
```
function School(name, minYears) {
  const self = this;
  if (!name && name.trim()) {
    throw Error("Не указано название школы");
  }

  if (!minYears && parseInt(minYears)) {
    throw new Error("Не указано минимальное количество лет");
  }

  this.MIN_YEARS = minYears;
  this.SCHOOL_NAME = name;

  this.checkAge = (age) => {
    if (age <= self.MIN_YEARS) {
      return {
        result: false,
        message: `Вам запрещено водить авто, вам должно быть ${self.MIN_YEARS} лет или больше`
      };
    } else if (age > self.MIN_YEARS) {
      return {
        result: true,
        message: `Добро пожаловать в автошколу "${self.SCHOOL_NAME}"`
      };
    }
  };

  this.getTeacherList = () => {
    return [
      "А. С. Иванов",
      "В. С. Петров",
      "И. А. Сидоров",
    ];
  }

  this.getTeacher = (id) => {
    id = id || Math.floor(Math.random() * self.getTeacherList().length);
    return self.getTeacherList()[id];
  };

  this.welcome = function askFunc(name, years) {
    const SCHOOL_ADDRESS = 'Санкт-Петербург, ул. Пушкина, дом 23';

    name = name || prompt('Как вас зовут?');

    if (!name) {
      alert('Вы не указали имя!');
      return askFunc(name, years);
    }

    years = years || Math.abs(parseFloat(prompt('Укажите ваш возраст')));

    if (!years) {
      alert('Вы не указали возраст!');
      return askFunc(name, years);
    }

    if (self.checkAge(years).result) {
      alert(self.checkAge(years).message + " " + name);
    } else if (!self.checkAge(years).result) {
      return alert(self.checkAge(years).message);
    }


    const TEACHER_NAME = self.getTeacher();

    alert(`Ваш преподаватель: ${TEACHER_NAME}\n\nЖдём вас по адресу: ${SCHOOL_ADDRESS}`)
    return;
  };

  return {
    welcome: this.welcome
  };
}

const autoSchool = new School('Парус', 18);

autoSchool.welcome();
autoSchool.welcome("Тест");
autoSchool.welcome("", 15);
autoSchool.welcome("Тест", 16);
autoSchool.welcome("Тест", 18);

