FFXIV-Send-KeyPress
===================

    class Send
    {
        #region Imports
        [DllImport("user32.dll")]
        static extern bool PostMessage(IntPtr hWnd, uint Msg, int wParam, int lParam);
        [DllImport("user32.dll", SetLastError = true)]
        static extern IntPtr FindWindow(string lpClassName, string lpWindowName);
        [DllImport("user32.dll", SetLastError = true)]
        static extern IntPtr FindWindowEx(IntPtr hwndParent, IntPtr hwndChildAfter, string lpszClass, string lpszWindow);
        #endregion

        public static void KeyPress(Keys key, int sleep = 100)
        {
            const int WM_KEYDOWN = 0x100;
            const int WM_KEYUP = 0x101;

            IntPtr ffxiv = FindWindow("ffxiv", null);
            IntPtr editx = FindWindowEx(ffxiv, IntPtr.Zero, "FFXIVGAME", null);

            PostMessage(editx, WM_KEYDOWN, (int)key, 0);
            Thread.Sleep(sleep);
            PostMessage(editx, WM_KEYUP, (int)key, 0);
        }
    }
