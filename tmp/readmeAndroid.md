package exam.sdsd;
import java.lang.reflect.*;
import android.app.*;
import android.content.*;
import android.os.*;
import android.telephony.*;
import android.view.*;
import android.view.View.OnClickListener;
import android.widget.*;

public class SamgTest extends Activity {
 
 Button on,off;
 EditText text;
 final ITelephony telephonyService; 
 
    
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        
   
        on = (Button)findViewById(R.id.on);
        off = (Button)findViewById(R.id.off);
	
	try{
		TelephonyAidl();
	}catch(Exception e){}
    }
    
    
    public void TelephonyAidl() throws Exception
    { 
     TelephonyManager tm = (TelephonyManager)getSystemService(TELEPHONY_SERVICE);
     @SuppressWarnings("rawtypes")
     Class c = Class.forName(tm.getClass().getName()); 
     Method m = c.getDeclaredMethod("getITelephony"); 
     m.setAccessible(true); 
     telephonyService = (ITelephony)m.invoke(tm); 
     
     on.setOnClickListener(new OnClickListener() {
      
      @Override
       public void onClick(View v) 
       {
        telephonyService.enableDataConnectivity();  
       }
      });
       
     off.setOnClickListener(new OnClickListener(){
      @Override
      public void onClick(View v) 
      {
       telephonyService.disableDataConnectivity();
      }
      });
   }
}
