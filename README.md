# Test
TestV.0.0.1 01-06-2561 
Cherry MySingleton
/**Call**/
/*try {
  MySingleton iSingleton = MySingleton.getInstance();
  ArrTsqMenuAll = iSingleton.getDataArray();
} catch (Exception e) {
	e.printStackTrace();
}
*/
package tg.wa.cm.bean;

import java.util.ArrayList;

import com.ibm.ws.batch.BatchJobExecutionEnvironmentConfig.beans.required;

import tg.wa.cm.dao.ThaiSquareNewDao;
import tg.wa.cm.model.ThaiSquare_menuModel;

public class MySingleton {
	
private static MySingleton instance = null;
    
    private MySingleton() {}

    private static ArrayList<ThaiSquare_menuModel> ArrTsqMenuAll = null;
    public static MySingleton getInstance() {
        if (instance == null) {
        	synchronized(MySingleton.class) {
        		if (instance == null)
        			instance = new MySingleton();
        	}
        }
        return instance;
    }

    /**
	 * Refresh singleton MySingleton
	 * 
	 * @return MySingleton
	 */
	public void refresh() throws Exception {

		ArrTsqMenuAll = getDataFromDB();
	}
	
    public ArrayList<ThaiSquare_menuModel> getDataArray()throws Exception {
    	
    	if (ArrTsqMenuAll == null) {

    		ArrTsqMenuAll = getDataFromDB(); 
		}
        return ArrTsqMenuAll;
    }

	private ArrayList<ThaiSquare_menuModel> getDataFromDB()throws Exception {
		if (ArrTsqMenuAll == null) {
			ArrTsqMenuAll = new ArrayList<ThaiSquare_menuModel>();
		} else {
			ArrTsqMenuAll.clear();
		}
		ThaiSquareNewDao dao = new ThaiSquareNewDao();	        
        ArrTsqMenuAll = dao.selectTHAISQUARE_MENUALL();
		
		return ArrTsqMenuAll;
		
	}
     
}
