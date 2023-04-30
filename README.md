# assignment01

### 우리 FISA 팀1 제출 문제입니다


### 목표
------
- 현실의 실제 사례를 예시로 객체지향에 대한 이해도를 높입니다.
- 클래스들간 상속 관계를 이해하고 업/다운캐스팅과 try-catch문을 활용합니다.
------
### 
- Mercedes Benz(이하 Benz) 라는 차 브랜드가 있습니다.
- Benz에는 AMG라는 브랜드가 있습니다.
- AMG의 모든 차량들은 "One man, One Engine" 이라는 모토에 따라 각각 한 명의 엔지니어가 할당됩니다.

![20230430091918](https://user-images.githubusercontent.com/114793764/235329506-558b97ab-987c-4254-9e58-d46b54c2d2b9.png)

- Car, Benz, AMG, Engineer 클래스들간의 상속관계를 활용하여 파일 주석에 적힌 문제를 풀어주세요.
------
``` java
public class Team01 {

	public static void main(String[] args) throws IOException {

		Engineer engineer1 = new Engineer("김엔진");
		Engineer engineer2 = new Engineer("정엔진");


		Benz benz = new Benz(200, "A-Class");
		AMG amg = new AMG(300, "G-Class 63 AMG", engineer1);




		//----------문제 1----------
		//다음 두 줄을 한 줄로 줄여주세요
		AMG temp = new AMG(522, "AMG_GT", engineer1);
		Car car = temp;



		//----------문제 2----------
		//car의 엔지니어를 [정엔진]씨로 바꾸고, 엔지니어의 이름을 출력해주세요



		//----------문제 3----------
		//car를 컴파일에러 없이 benzList에 추가하고, 모델명을 출력해주세요
		ArrayList<Benz> benzList = new ArrayList<>();
		benzList.add(benz);
		benzList.add(amg);
		//benzList.add(car);
    
    
    
		//---------------문제 4---------------
		//논리적 예외 1 -> 예외가 발생하는 경우를 말해주세요
		System.out.print("몇 번째 차를 조회할까요? : ");
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));

		boolean flag1 = true;
		do {
			try{
				int n = Integer.parseInt(bf.readLine());
				Benz myBenz = benzList.get(n);
				System.out.println("모델명 : " + myBenz.model + "\n");
				flag1 = false;
			}catch(NumberFormatException e){
				System.out.print("숫자를 입력하세요 : ");
			}catch (IndexOutOfBoundsException e) {
				System.out.print("해당 차가 존재하지 않습니다. 다시 입력하세요 : ");
			}
		}while(flag1);
		//------------------------------------



		//---------------문제 5---------------
		//논리적 예외 2 -> 예외가 발생하는 경우를 말해주세요
		boolean flag2 = true;
		do {
			try {
				System.out.print("마력을 입력하세요 : ");
				int inputHP = Integer.parseInt(bf.readLine());
				Benz yourBenz = new Benz(inputHP, "님이 산 차");
				System.out.println(yourBenz.model + "의 마력은 " + yourBenz.HP + " 입니다.");
				flag2 = false;
			}catch(NumberFormatException e){
				System.out.print("숫자를 입력하세요 : ");
			}catch(Exception e) {
				System.out.print("님이 산 차의 " + e.getMessage() + "\n다시 입력하세요 : ");
			}
		}while(flag2);
		//------------------------------------

	}

}


class Engineer{
	String name;
	Engineer(String name){
		this.name = name;
	}
}

class Car {
	int HP;
	public Car(int HP) {
		if(HP<=0) {
			throw new RuntimeException("마력은 0이나 음수가 될 수 없습니다.");
		}
		this.HP = HP;
	}
}

//상위 클래스에 매개변수가 있는 생성자 존재하기에 기본생성자 생성 불가
class Benz extends Car {
	String model;
	public Benz(int HP, String model) {
		super(HP);
		this.model = model;
	}
}

//상위 클래스에 매개변수가 있는 생성자 존재하기에 기본생성자 생성 불가
class AMG extends Benz{
	Engineer engineer;

	public AMG(int HP, String model, Engineer engineer) {
		super(HP, model);
		this.engineer = engineer;
	}

	public String getEngineerName() {
		return engineer.name;
	}
}
```
