```mermaid
graph TD
A[Start] --> B{Setup};
subgraph Initialization
B --> C[LCD Initialize];
C --> D[ADMUX: Set AVCC Ref and Channel A1];
D --> E[ADCSRA: Set Prescaler 128 and Enable ADC];
end
E --> F((Loop));
subgraph MainLoop
F --> G[Start Conversion: Set ADCSRA Bit ADSC];
G --> H{Wait: Is ADSC Bit Cleared?};
H -- No --> G;
H -- Yes --> I[Read 10-bit Result from ADCL and ADCH];
I --> J[Calculate Celsius];
end
J --> K[Output: Print Temp to LCD and Serial Monitor];
K --> L[Delay 1000ms];
L --> F;
