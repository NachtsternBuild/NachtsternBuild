# NachtsternBuild

> *"Always building, always learning."*  

```c
/** 
 * nachtstern.c — "NachtsternBuild Orbiter" 
 * A tiny, fun C program that prints a pastel-ish animated header
 * Compile: gcc -O2 -std=c11 -o nachtstern nachtstern.c
 * Run: ./nachtstern
 */
#define _XOPEN_SOURCE 500 // for usleep
#define SLEEP_US 80000

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>   /* usleep */
#include <time.h>


/**
* ANSI color helpers (pastel-like) 
*/
static const char *cols[] = {
    "\x1b[38;5;159m", /* pastel cyan */
    "\x1b[38;5;175m", /* pastel purple */
    "\x1b[38;5;180m", /* pastel blue */
    "\x1b[38;5;216m", /* pastel orange */
    "\x1b[38;5;157m"  /* pastel green */
};

static const char *RESET = "\x1b[0m";
static const int NCOLS = sizeof(cols)/sizeof(cols[0]);

/**
* Simple spinner frames 
*/
static const char *frames[] = { "⠁","⠂","⠄","⡀","⢀","⠠","⠐","⠈" };
static const int NFRAMES = sizeof(frames)/sizeof(frames[0]);

/**
* Draw a fancy title using colors 
*/
void draw_title(int phase) 
{
    const char *name = "NachtsternBuild";
    int len = (int)strlen(name);
    printf("\r");
    for (int i = 0; i < len; ++i) 
    {
        const char *c = cols[(i + phase) % NCOLS];
        putchar(0); // no-op to keep char alignment in some terminals 
        printf("%s%c%s", c, name[i], RESET);
    }
}

/**
* A small "orbiter" line with spinner and progress-like dots 
*/
void orbiter(int step) 
{
    int pos = step % 40;
    for (int i = 0; i < 40; ++i) 
    {
        if (i == pos) 
        {
            printf("%s●%s", cols[(step/3) % NCOLS], RESET);
        }
        
        else 
        {
            if (i % 5 == 0) 
            {
                printf("·");  // use UTF-8 dot
            } 
            
            else 
            {
                putchar(' ');
            }
        }
    }
}

/**
* A fake "updater" that alternates success/fail cheekily 
*/
void fake_update_sequence(void) 
{
    const char *msgs[] = {
        "Scanning modules...",
        "Patching fastboot-assistant...",
        "Repacking Treble image...",
        "Optimizing AtlantisOS...",
        "Tidying Experimente..."
    };
    int n = sizeof(msgs)/sizeof(msgs[0]);
    for (int i = 0; i < n; ++i) 
    {
        printf("\n  %s ", msgs[i]);
        fflush(stdout);
        for (int t = 0; t < 10; ++t) 
        {
            printf("%s%s%s", cols[(i+t) % NCOLS], frames[(i+t) % NFRAMES], RESET);
            fflush(stdout);
            usleep(SLEEP_US);
            printf("\b \b");
        }
        /**
        * playful outcome 
        */
        if ((i % 2) == 0) 
        {
            printf("%s[OK]%s", cols[(i+2) % NCOLS], RESET);
        } 
        
        else 
        {
            printf("%s[skipped — user debug pending]%s", cols[(i+4) % NCOLS], RESET);
        }
    }
    printf("\n\n");
}

int main(void) 
{
    /**
	 * hide cursor 
	 */
    printf("\x1b[?25l");
    for (int phase = 0; phase < 12; ++phase) 
    {
        /**
		 * print title 
		 */
        printf("\r");
        const char *header = "  •  ";
        printf("%s", header);
        for (int i = 0; i < (int)strlen("NachtsternBuild"); ++i) 
        {
            printf("%s%c%s", cols[(i + phase) % NCOLS], "NachtsternBuild"[i], RESET);
        }
        printf("  ");
        /**
		 * spinner 
		 */
        printf("%s%s%s", cols[phase % NCOLS], frames[phase % NFRAMES], RESET);
        fflush(stdout);
        usleep(SLEEP_US * 6);
    }

    /**
	 * orbiter animation 
	 */
    for (int i = 0; i < 80; ++i) 
    {
        printf("\r ");
        orbiter(i);
        fflush(stdout);
        usleep(SLEEP_US);
    }

    /**
	 * fake update 
	 */
    printf("\n\n");
    fake_update_sequence();

    /**
	 * final playful tagline 
	 */
    printf("%s Done — build something weird and useful. %s\n", cols[2], RESET);

    /**
	 * restore cursor 
	 */
    printf("\x1b[?25h");
    return 0;
}
```

## Languages & Tools & Insights
<p align="center">
  <img src="https://github.com/devicons/devicon/blob/master/icons/c/c-original.svg" title="C" alt="C" width="96" height="96" style="margin: 10px;"/>
  <img src="https://github.com/devicons/devicon/blob/master/icons/bash/bash-plain.svg" title="Bash" alt="Bash" width="96" height="96" style="margin: 10px;"/> 
  <img src="https://github.com/devicons/devicon/blob/master/icons/python/python-original.svg" title="Python" alt="Python" width="96" height="96" style="margin: 10px;"/> 
  <img src="https://github.com/devicons/devicon/blob/master/icons/java/java-original.svg" title="Java" alt="Java" width="96" heigth="96" style="margin: 10px"/>
  <img src="https://github.com/devicons/devicon/blob/master/icons/linux/linux-original.svg" title="Linux" alt="Linux" width="96" height="96" style="margin: 10px;"/> 
  <img src="https://github.com/devicons/devicon/blob/master/icons/ubuntu/ubuntu-original.svg" title="Ubuntu" alt="Ubuntu" width="96" height="96" style="margin: 10px;"/> 
  <img src="https://github.com/devicons/devicon/blob/master/icons/android/android-original.svg" title="Android" alt="Android" width="96" height="96" style="margin: 10px;"/> 
</p>
<p align="center">
  <img src="http://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=NachtsternBuild&theme=2077" height="180em" style="border-radius: 20px;"/>
</p>

<p align="center">
  <img src="http://github-profile-summary-cards.vercel.app/api/cards/stats?username=NachtsternBuild&theme=2077" height="180em" style="border-radius: 20px;"/>
  <img src="http://github-profile-summary-cards.vercel.app/api/cards/productive-time?username=NachtsternBuild&theme=2077" height="180em" style="border-radius: 20px;"/>
</p>
