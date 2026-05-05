When we open a game the process is like this:
1. load some files 
2. create some objects 
3. download sounds/videos
4. clean temporary files 
5. load saves 

But, if we have two different games, where the behavior of a single step differs, we need to completely rewrite all the steps and just change one step which differs. 

Instead of doing so we just create a template:
1. *base class* 
```java
public abstract class BaseGameLoader {
	public void load() {
		byte[] data = loadLocalData();
		createObjects(data);
		downloadAdditionalFiles();
		cleanTempFiles();
		initializeProfiles();
	}
	
	abstract byte[] loadLocalData();
	abstract void createObjects(byte[] data);
	abstract void downloadAdditionalFiles();
	abstract void cleanTempFiles();
	abstract void initializeProfiles();
	
	protected void cleanTempFiles() {
		System.out.println("Cleaning temporary files...")
		// Some code
	}
}
```

2. *concrete class*
```java
public class WorldOfWarcraftLoader extends BaseGameLoader {
	@Override
	byte[] loadLocalData() {
		//Actual impl
	}
	
	@Override
	void createObjects(byte[] data) {
		//Actual impl
	}
	
	@Override
	void downloadAdditionalFiles() {
		//Actual impl
	}
	
	@Override
	void initializeProfiles() {
		//Actual impl
	}
}
```