Program for Automatic Lighting System

#define F_CPU 8000000UL //telling controller crystal frequency 
#include <avr/io.h> //header to enable data flow control over pins
#include <util/delay.h> //header to enable delay function in program

int temp=0;
int delay=1;
int main(void)
{
    DDRA= 0b//PB4 is used as output
    DDRB = 0b00000000; //PB3 is used as input 
    
    int x=0; // taking a integer 
    while(1)
    {
        if (bit_is_set(PINB,0)) //When there is motion (motion sensor gives high output on presence of human being)
        {
            x=1; //set x when condition is satisfied
        }
    
        {
             if (x==1) //when x is set
            {
                 PORTB |=(1<<PINB2); //trigger transistor to drive power led
                _delay_ms(220); //wait 220ms (can be changed for higher duration)
                PORTB &=~(1<<PINB2); //turn on transistor trigger
                x=0; // reset x 
            }
        }
}