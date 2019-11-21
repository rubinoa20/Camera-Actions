#include <kipr/botball.h>
int orange = 0;
int green = 1;
int blue = 2;
int middle = 80;
int servo = 0;
int orange_servo = 500;
int blue_servo = 1500;
int reset = 1024;
int l_motor = 0; 
int r_motor = 3;
int forward = 55;
int backward = -55;
int pause = 1000;
int main()
{
camera_open();
while (digital(8) == 0)
{
camera_update();
if (get_object_count(orange) > 0)
{
    printf("Orange poms counted= %d\n", get_object_count(orange));
	printf("Orange poms X= %d\n", get_object_center_x(orange, 0));
    orange_detected();
}
if (get_object_count(green) > 0)
{
    printf("Green poms counted= %d\n", get_object_count(green));
	printf("Green poms X= %d\n", get_object_center_x(green, 0));
    green_detected();
}
if (get_object_count(blue) > 0)
{
    printf("Blue poms counted= %d\n", get_object_count(blue));
	printf("Blue poms X= %d\n", get_object_center_x(blue, 0));
    blue_detected();
}
}
camera_close();
return 0;
}

//FUNCTION DEFINITIONS//
void forwards(){
    motor(l_motor,forward);
    motor(r_motor,forward);
    msleep(pause);
    ao();
}
void backwards(){
 	motor(l_motor,backward);
    motor(r_motor,backward);
    msleep(100);
    ao();
}
void orange_detected(){
    enable_servos();
    set_servo_position(servo, orange_servo);
    msleep(pause);
    set_servo_position(servo, reset);
    msleep(pause);
    disable_servos();
}
void blue_detected(){
    backwards();
}
void green_detected(){
    enable_servos();
    set_servo_position(servo, blue_servo);
    msleep(pause);
    set_servo_position(servo, reset);
    msleep(pause);
    disable_servos();
}
