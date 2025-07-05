# OSIINFO
Information gathering tool for Insta 
import instaloader

def gather_instagram_info(username):
    loader = instaloader.Instaloader()

    try:
        profile = instaloader.Profile.from_username(loader.context, username)

        data = {
            "Username": profile.username,
            "Full Name": profile.full_name,
            "Bio": profile.biography,
            "Followers": profile.followers,
            "Following": profile.followees,
            "Total Posts": profile.mediacount,
            "External URL": profile.external_url,
            "Is Verified": profile.is_verified,
            "Is Private": profile.is_private
        }

        with open(f"{username}_info.txt", "w", encoding="utf-8") as f:
            for key, value in data.items():
                f.write(f"{key}: {value}\n")

        print(f"[+] Data saved to {username}_info.txt")

    except Exception as e:
        print("[-] Error:", e)

if __name__ == "__main__":
    print("=== OSIINFO - Instagram OSINT Tool ===")
    user_input = input("Enter Instagram username: ")
    gather_instagram_info(user_input)
