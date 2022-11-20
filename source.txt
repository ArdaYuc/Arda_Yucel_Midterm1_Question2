#define rccahblenR * ( (unsigned volatile int *)0x40023830)
#define gpiodmask 1<<3
#define gpiodModr *((unsigned volatile int* )0x40020c00)
#define gpiodP14mask 1<<28
#define gpiodP13mask 1<<26
#define gpiodP15mask 1<<30
#define gpiodP12mask 1<<24
#define gpiodOdr  *((unsigned volatile int *)0x40020c14)
#define gpiodp14onmask 1<<14
#define gpiodp14ofmask 0<<14
#define gpiodp13onmask 1<<13
#define gpiodp13ofmask ~(1<<13)
#define gpiodp15onmask 1<<15
#define gpiodp15ofmask 0<<15
#define gpiodp12onmask 1<<12
#define gpiodp12ofmask 0<<12
int a=0;
int y=0;

// led12 = yeşil led13 = turuncu led14 = kırmızı led15 = mavi

void init_leds ();
void turn_name_on();
void turn_surname_on();
void turn_name_off();
void turn_surname_off();
void delayy();

//Arda Yucel.
//a+r+d+a ascii değerleri için 408 oluyor.
//408 mod 4=0 kırmızı led
//y+u+c+e+l ascii değerleri için 546 oluyor.
//546 mod 4=2 turuncu led

void init_leds(){

rccahblenR = gpiodmask;
gpiodModr=gpiodP14mask;
gpiodModr |=gpiodP13mask;

}

void turn_name_on(){

gpiodOdr=gpiodp14onmask;

}
void turn_name_off(){

gpiodOdr&=gpiodp14ofmask;

}
void turn_surname_on(){

gpiodOdr|=gpiodp13onmask;

}
void turn_surname_off(){

gpiodOdr&=gpiodp13ofmask;

}

void delayy(){
for(int i=0;i<0x00000FFF;i++){

}
}


int main() {

init_leds();

while(a<4){
	turn_name_on();
	delayy();
	delayy();
	turn_name_off();
	a = a+1;

}


while(y<5){
	turn_surname_on();
	delayy();
	delayy();
	turn_surname_off();
	y = y+1;

}

return 0;
}


