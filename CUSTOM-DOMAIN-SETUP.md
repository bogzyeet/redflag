# 🌐 Custom Domain Setup Guide - IONOS to GitHub Pages

## 📋 What You Need
- Your domain from IONOS (e.g., redflag.club)
- Access to IONOS DNS settings
- Your GitHub repository (already set up ✅)

---

## 🎯 Setup Process (Two Parts)

### Part 1: GitHub Pages Configuration

#### Step 1: Update CNAME File
1. **Open the `CNAME` file** in your repository
2. **Replace** `yourdomain.com` with your actual domain
   ```
   redflag.club
   ```
   (or whatever your IONOS domain is)

3. **Save the file**

#### Step 2: Commit and Push
```bash
git add CNAME
git commit -m "Add custom domain"
git push
```

#### Step 3: Configure on GitHub
1. Go to: https://github.com/bogzyeet/redflag/settings/pages
2. Scroll to **"Custom domain"** section
3. Enter your domain: `redflag.club`
4. Click **"Save"**
5. ✅ Check **"Enforce HTTPS"** (after DNS propagates)

---

### Part 2: IONOS DNS Configuration

#### Option A: Apex Domain (redflag.club)

**Configure A Records:**
1. Log in to **IONOS Control Panel**
2. Go to **Domains & SSL**
3. Click on your domain
4. Go to **DNS Settings**
5. Add these **A Records**:

```
Type: A
Host: @
Points to: 185.199.108.153
TTL: 3600

Type: A
Host: @
Points to: 185.199.109.153
TTL: 3600

Type: A
Host: @
Points to: 185.199.110.153
TTL: 3600

Type: A
Host: @
Points to: 185.199.111.153
TTL: 3600
```

**Add CNAME for www:**
```
Type: CNAME
Host: www
Points to: bogzyeet.github.io
TTL: 3600
```

#### Option B: Subdomain (www.redflag.club)

**If you prefer www subdomain:**
```
Type: CNAME
Host: www
Points to: bogzyeet.github.io
TTL: 3600
```

---

## 🔧 IONOS Specific Steps

### Detailed IONOS Configuration

1. **Login to IONOS:**
   - Go to https://www.ionos.com
   - Click "Login"
   - Enter your credentials

2. **Navigate to DNS:**
   - Click on **"Domains & SSL"**
   - Select your domain from the list
   - Click **"DNS"** or **"Manage DNS"**

3. **Add DNS Records:**
   - Click **"Add Record"** or **"+"**
   - Select record type: **"A"** or **"CNAME"**
   - Fill in the details from above
   - Click **"Save"**

4. **Repeat for All Records:**
   - Add all 4 A records
   - Add the www CNAME record

### IONOS Screenshot Guide

```
┌─────────────────────────────────────┐
│  IONOS DNS Management               │
├─────────────────────────────────────┤
│                                     │
│  Record Type: A                     │
│  Hostname: @                        │
│  IP Address: 185.199.108.153       │
│  TTL: 3600                          │
│                                     │
│  [Add Record]                       │
└─────────────────────────────────────┘
```

---

## ⏱️ DNS Propagation

### Timeline
- **Minimum:** 15 minutes
- **Average:** 1-2 hours
- **Maximum:** 24-48 hours

### Check Propagation
Use these tools:
- https://dnschecker.org
- https://www.whatsmydns.net
- Command line: `nslookup yourdomain.com`

---

## ✅ Verification Steps

### 1. Check DNS Records
```bash
# Check A records
nslookup yourdomain.com

# Check CNAME
nslookup www.yourdomain.com
```

### 2. Check GitHub Pages
1. Go to: https://github.com/bogzyeet/redflag/settings/pages
2. You should see:
   ```
   ✅ DNS check successful
   Your site is published at https://yourdomain.com
   ```

### 3. Test Your Site
- Visit: `http://yourdomain.com`
- Visit: `http://www.yourdomain.com`
- Visit: `https://yourdomain.com` (after HTTPS is enabled)

---

## 🎯 Complete DNS Configuration Example

### For domain: redflag.club

```
Type    Host    Value                   TTL
────────────────────────────────────────────
A       @       185.199.108.153        3600
A       @       185.199.109.153        3600
A       @       185.199.110.153        3600
A       @       185.199.111.153        3600
CNAME   www     bogzyeet.github.io     3600
```

---

## 🔒 Enable HTTPS (After DNS Propagates)

1. Wait for DNS to propagate (check with dnschecker.org)
2. Go to GitHub Pages settings
3. Check **"Enforce HTTPS"**
4. Wait a few minutes for certificate generation
5. ✅ Your site will be available at `https://yourdomain.com`

---

## 🚨 Troubleshooting

### Issue: "DNS check unsuccessful"
**Solution:**
- Wait longer (DNS propagation can take 24-48 hours)
- Double-check A records are correct
- Make sure @ is used for hostname (not blank)

### Issue: "Certificate generation failed"
**Solution:**
- Uncheck and re-check "Enforce HTTPS"
- Wait 24 hours after DNS propagates
- Ensure all 4 A records are present

### Issue: "Site not loading"
**Solution:**
- Check CNAME file has correct domain
- Verify DNS records on IONOS
- Clear browser cache (Ctrl + F5)
- Try incognito/private mode

### Issue: "www not working"
**Solution:**
- Ensure CNAME record for www is added
- Check it points to `bogzyeet.github.io`
- Wait for DNS propagation

---

## 📝 Quick Reference - IONOS DNS Settings

### What You Need to Add:

**4 A Records (for apex domain):**
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**1 CNAME Record (for www):**
```
www → bogzyeet.github.io
```

---

## 🎨 Visual Guide

### Before (GitHub subdomain):
```
https://bogzyeet.github.io/redflag/
         ↓ DNS SETUP ↓
https://redflag.club/
```

### After (Custom domain):
```
https://redflag.club           ✅ Your custom domain
https://www.redflag.club       ✅ With www
https://bogzyeet.github.io/redflag/  ↪️ Redirects to custom
```

---

## 📞 Need Help?

### IONOS Support
- Phone: Check your IONOS dashboard
- Chat: Available in IONOS control panel
- Docs: https://www.ionos.com/help

### GitHub Pages
- Docs: https://docs.github.com/pages
- Custom domains: https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site

---

## ✨ Final Steps

1. ✅ Update CNAME file with your domain
2. ✅ Push to GitHub
3. ✅ Add DNS records on IONOS
4. ✅ Wait for propagation (1-48 hours)
5. ✅ Enable HTTPS on GitHub
6. ✅ Test your site!

**Your Red Flag Club site will be live at your custom domain!** 🎉

