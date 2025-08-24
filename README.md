original projet of https://github.com/cifertech

Library TFT_eSPI

open : User_Setup.h:


add :



#define TOUCH_INVERT_X   false   // true = inverti X, false = normale
      
      
#define TOUCH_INVERT_Y   true   // true = inverti Y, false = normale


      
//////////////////////////////////////////////////////////////////////////////////////////////////////



open : TFT_eSPI/Extensions/Touch.h

replace 

void TFT_eSPI::convertRawXY(uint16_t *x, uint16_t *y)
{
  uint16_t x_tmp = *x, y_tmp = *y, xx, yy;

  if(!touchCalibration_rotate){
    xx = (x_tmp - touchCalibration_x0) * _width / touchCalibration_x1;
    yy = (y_tmp - touchCalibration_y0) * _height / touchCalibration_y1;
  } else {
    xx = (y_tmp - touchCalibration_x0) * _width / touchCalibration_x1;
    yy = (x_tmp - touchCalibration_y0) * _height / touchCalibration_y1;
  }

  // Applica inversioni opzionali da User_Setup
  if(touchCalibration_invert_x || defined(TOUCH_INVERT_X) && TOUCH_INVERT_X) xx = _width - xx;
  if(touchCalibration_invert_y || defined(TOUCH_INVERT_Y) && TOUCH_INVERT_Y) yy = _height - yy;

  *x = xx;
  *y = yy;
}








///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

void setup() 

add:

Wire.begin(35, 4); // SDA=4, SCL=35 

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
