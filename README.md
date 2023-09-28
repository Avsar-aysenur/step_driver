#include <Step_ISHE.h>

#define analogInPin1 PIN_A1 // RA1 pot

#define BACKWARD PIN_B5 // RA0
#define FORWARD  PIN_B4 // RA2
#define ON_OFF   PIN_B3 // RA3

#define LED_FORWARD  PIN_C4 // RC4
#define LED_BACKWARD PIN_C5 // RC5

#define A_H_Q1  PIN_D0 //  RC2
#define A_L_Q2  PIN_D1 //  RC1
#define A2_H_Q3 PIN_D2 //  RC3
#define A2_L_Q4 PIN_D3 //  RC2
#define B_H_Q5  PIN_D4 //  RC5
#define B_L_Q6  PIN_D5 //  RC4
#define B2_H_Q7 PIN_D6 //  RC6
#define B2_L_Q8 PIN_D7 //  RC7

int16 x = 100;
//int16 analogBilgi; // Okuduğumuz analog değeri bu değişkene aktaracağız

void FORWARD (){

  output_high(A_H_Q1) ; //1000
  output_high(A2_L_Q4);
  delay_ms(x);

  output_high(A_H_Q1) ; //1100
  output_high(A2_L_Q4);
  output_high(A_L_Q2) ;
  output_high(A2_H_Q3);
  delay_ms(x);

  output_low(A_H_Q1) ;
  output_low(A2_L_Q4);
  delay_ms(x);

  output_high(A_L_Q2) ; //0100
  output_high(A2_H_Q3);
  delay_ms(x);

  output_high(A_L_Q2) ; //0110
  output_high(A2_H_Q3);
  output_high(B_L_Q6) ;
  output_high(B2_H_Q7);
  delay_ms(x);

  output_low(A_L_Q2) ;
  output_low(A2_H_Q3);
  delay_ms(x);
  
  output_high(B_L_Q6) ; //0010
  output_high(B2_H_Q7);  
  delay_ms(x);

  output_high(B_H_Q5) ; //0011
  output_high(B_L_Q6) ;
  output_high(B2_H_Q7);
  output_high(B2_L_Q8);
  delay_ms(x);

  output_low(B_L_Q6) ;
  output_low(B2_H_Q7);
  delay_ms(x);

  output_high(B_H_Q5) ; //0001
  output_high(B2_L_Q8);
  delay_ms(x);
  
  output_high(B_H_Q5) ; //1001
  output_high(B2_L_Q8);
  output_high(A_H_Q1) ;
  output_high(A2_L_Q4);
  delay_ms(x);

  output_low(B_H_Q5);
  output_low(B2_L_Q8);
  delay_ms(x);
}

void BACKWARD (){

  output_high(A_H_Q1) ; //1001
  output_high(A2_L_Q4);
  output_high(B_H_Q5) ;
  output_high(B2_L_Q8);
  delay_ms(x);
  
  output_low(A_H_Q1) ;
  output_low(A2_L_Q4);
  delay_ms(x);

  output_high(B_H_Q5) ; //0001
  output_high(B2_L_Q8);
  delay_ms(x);

  output_high(B_H_Q5) ; //0011 
  output_high(B2_L_Q8);
  output_high(B_L_Q6) ;
  output_high(B2_H_Q7);
  delay_ms(x);
  
  output_low(B_H_Q5) ;
  output_low(B2_L_Q8);
  delay_ms(x);

  output_high(B_L_Q6) ; //0010
  output_high(B2_H_Q7);
  delay_ms(x);

  output_high(A_L_Q2) ; //0110
  output_high(A2_H_Q3);
  output_high(B_L_Q6) ;
  output_high(B2_H_Q7);
  delay_ms(x);
  
  output_low(B_L_Q6) ;
  output_low(B2_H_Q7);
  delay_ms(x);
 
  output_high(A_L_Q2) ; //0100
  output_high(A2_H_Q3);
  delay_ms(x);

  output_high(A_L_Q2) ; //1100
  output_high(A2_H_Q3);
  output_high(A_H_Q1) ;
  output_high(A2_L_Q4);
  delay_ms(x);
  
  output_low(A_L_Q2) ;
  output_low(A2_H_Q3);
  delay_ms(x);

  output_high(A_H_Q1) ; //1000
  output_high(A2_L_Q4);
  delay_ms(x);   
   
}

void main()
{
   setup_adc_ports(AN0_AN1_AN3);
   setup_adc(ADC_CLOCK_DIV_32);
      
   set_tris_b(0b00111000);
   set_tris_d(0x00);
   output_d(0x00);
   set_tris_c(0x00);
   
   output_c(0xff);
   delay_ms(500);
   output_c(0x00);
   delay_ms(500);
  
   while(TRUE)
   
   {
  
  /*set_adc_channel(1); // AN1 numaralı kanaldan okuma yapacağımızı belirttik
    analogBilgi = read_adc(); // AN! numaralı kanaldan analog değeri oku
    delay_ms(1); // 0.01 saniye bekle
    x = analogBilgi;*/
   
   if(input(PIN_B3)==0){
   
   output_high(PIN_C4);
   output_low(PIN_C5);
   ileri ();
   
   }
   if(input(PIN_B3)==1){
   
   output_high(PIN_C5);
   output_low(PIN_C4);
   geri ();
   
   }
   
   }}
