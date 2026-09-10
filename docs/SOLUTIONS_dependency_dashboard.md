import sys
import os

# Fix for UnicodeEncodeError: Explicitly set stdout encoding to UTF-8 
# This is necessary because many environments (especially Windows consoles) default 
# to non-Unicode codepages (like cp1254), causing emojis and certain special characters to fail.
if sys.stdout.encoding != 'utf-8':
    try:
        sys.stdout.reconfigure(encoding='utf-8')
    except AttributeError:
        # For older Python versions or environments where reconfigure fails
        pass

def validate_version_compatibility(lockfile, pkg, new_version):
    """
    Simulates checking version compatibility and printing status messages.
    The original error occurred within the print statement here.
    """
    print("--- Starting Compatibility Check ---")
    if not lockfile:
        return False

    updated_pkg = f"{pkg}_v{new_version}"

    # The fix relies on the sys.stdout reconfigure above, allowing this line to pass UTF-8 characters.
    print(f"\u2705 {updated_pkg} v{new_version} seems stable based on basic checks.")
    return True

if __name__ == "__main__":
    # Placeholder definition mimicking the variables used in the traceback
    DUMMY_LOCKFILE = "dummy.lock" 
    
    # The line that caused the failure (now corrected by environment setup)
    print("\nRunning verification process...")
    next_valid = validate_version_compatibility(DUMMY_LOCKFILE, "temp", "15.5.18")

    if next_valid:
        print("Verification successful.")
    else:
        print("Verification failed.")
