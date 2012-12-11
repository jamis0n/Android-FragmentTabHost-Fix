Android-FragmentTabHost-Fix
===========================

Modified version of FragmentTabHost, allowing manual assignment of TabHost layout

The latest release of the Android Support Library v17 has a new layout object called FragmentTabHost,
which allows a TabHost to be embedded in a Fragment.

Unfortunately, the code to check for an existing TabHost in the setup() function doesn't work.

This file, MyFragmentTabHost.java, is a copy of the original file, omitting the code which creates a new layout
object for the TabHost. As such, it is required to specify a layout object before initializing the TabHost:

MyFragment.java

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.mylayout, null);
        mTabHost = (MyFragmentTabHost) view.findViewById(android.R.id.tabhost);
        mTabHost.setup(getActivity(), getChildFragmentManager(), android.R.id.tabcontent);
      
        ...
        ... ADD TABS HERE
        ...
      }
      
The XML file included sets the tabs in the fragment on the bottom.