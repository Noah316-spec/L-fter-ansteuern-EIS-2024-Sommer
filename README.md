# L-fter-ansteuern-

Eine mögliche schleife um die temperatur bzw. Luftfeuchtikeit abzufragen und
wenn das stimmt wird je nach bereich leds und lüfter angestellt.

```
while(1)
{
        adc_humid = adc_readvoltage(0);
        _delay_ms(10);
        adc_temp = adc_readvoltage(1);
        if ((adc_temp <= 22) && (adc_temp >= 20) && (adc_humid <= 60) && (adc_humid >= 40)){
            leds = 0b01111111;
            mcp4725_setvoltage_fastmode(1,0); // Läuft nicht 
        }else if (((adc_temp < 20) && (adc_temp >= 16)) || ((adc_humid < 40) && (adc_humid >= 30)) || ((adc_temp > 22) && (adc_temp <= 26)) || ((adc_humid > 60) && (adc_humid <= 70))){
            leds = 0b10111111;
            mcp4725_setvoltage_fastmode(1,2.5); // läuft halb
        }else if (((adc_temp < 16) || (adc_humid < 30)  || (adc_temp > 26) || (adc_humid > 70)) && (leds == 0b10111111)){
            leds = 0b11011111;
            mcp4725_setvoltage_fastmode(1,5); // läuft voll
        }else{
            leds = 0b11011111;
            }
}
