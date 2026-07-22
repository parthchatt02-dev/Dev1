{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "import pandas as pd\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "data = pd.read_csv('sgemm_product.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>MWG</th>\n",
       "      <th>NWG</th>\n",
       "      <th>KWG</th>\n",
       "      <th>MDIMC</th>\n",
       "      <th>NDIMC</th>\n",
       "      <th>MDIMA</th>\n",
       "      <th>NDIMB</th>\n",
       "      <th>KWI</th>\n",
       "      <th>VWM</th>\n",
       "      <th>VWN</th>\n",
       "      <th>STRM</th>\n",
       "      <th>STRN</th>\n",
       "      <th>SA</th>\n",
       "      <th>SB</th>\n",
       "      <th>Run1 (ms)</th>\n",
       "      <th>Run2 (ms)</th>\n",
       "      <th>Run3 (ms)</th>\n",
       "      <th>Run4 (ms)</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>115.26</td>\n",
       "      <td>115.87</td>\n",
       "      <td>118.55</td>\n",
       "      <td>115.80</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>78.13</td>\n",
       "      <td>78.25</td>\n",
       "      <td>79.25</td>\n",
       "      <td>79.19</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>79.84</td>\n",
       "      <td>80.69</td>\n",
       "      <td>80.76</td>\n",
       "      <td>80.97</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>84.32</td>\n",
       "      <td>89.90</td>\n",
       "      <td>86.75</td>\n",
       "      <td>85.58</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>115.13</td>\n",
       "      <td>121.98</td>\n",
       "      <td>122.73</td>\n",
       "      <td>114.81</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   MWG  NWG  KWG  MDIMC  NDIMC  MDIMA  NDIMB  KWI  VWM  VWN  STRM  STRN  SA  \\\n",
       "0   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "1   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "2   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "3   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "4   16   16   16      8      8      8      8    2    1    1     0     1   0   \n",
       "\n",
       "   SB  Run1 (ms)  Run2 (ms)  Run3 (ms)  Run4 (ms)  \n",
       "0   0     115.26     115.87     118.55     115.80  \n",
       "1   1      78.13      78.25      79.25      79.19  \n",
       "2   0      79.84      80.69      80.76      80.97  \n",
       "3   1      84.32      89.90      86.75      85.58  \n",
       "4   0     115.13     121.98     122.73     114.81  "
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(241600, 18)"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 241600 entries, 0 to 241599\n",
      "Data columns (total 18 columns):\n",
      "MWG          241600 non-null int64\n",
      "NWG          241600 non-null int64\n",
      "KWG          241600 non-null int64\n",
      "MDIMC        241600 non-null int64\n",
      "NDIMC        241600 non-null int64\n",
      "MDIMA        241600 non-null int64\n",
      "NDIMB        241600 non-null int64\n",
      "KWI          241600 non-null int64\n",
      "VWM          241600 non-null int64\n",
      "VWN          241600 non-null int64\n",
      "STRM         241600 non-null int64\n",
      "STRN         241600 non-null int64\n",
      "SA           241600 non-null int64\n",
      "SB           241600 non-null int64\n",
      "Run1 (ms)    241600 non-null float64\n",
      "Run2 (ms)    241600 non-null float64\n",
      "Run3 (ms)    241600 non-null float64\n",
      "Run4 (ms)    241600 non-null float64\n",
      "dtypes: float64(4), int64(14)\n",
      "memory usage: 33.2 MB\n"
     ]
    }
   ],
   "source": [
    "data.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "MWG          0\n",
       "NWG          0\n",
       "KWG          0\n",
       "MDIMC        0\n",
       "NDIMC        0\n",
       "MDIMA        0\n",
       "NDIMB        0\n",
       "KWI          0\n",
       "VWM          0\n",
       "VWN          0\n",
       "STRM         0\n",
       "STRN         0\n",
       "SA           0\n",
       "SB           0\n",
       "Run1 (ms)    0\n",
       "Run2 (ms)    0\n",
       "Run3 (ms)    0\n",
       "Run4 (ms)    0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [],
   "source": [
    "data['Mean_Runtime'] = (data['Run1 (ms)'] + data['Run2 (ms)'] + data['Run3 (ms)'] + data['Run4 (ms)'])/4"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>MWG</th>\n",
       "      <th>NWG</th>\n",
       "      <th>KWG</th>\n",
       "      <th>MDIMC</th>\n",
       "      <th>NDIMC</th>\n",
       "      <th>MDIMA</th>\n",
       "      <th>NDIMB</th>\n",
       "      <th>KWI</th>\n",
       "      <th>VWM</th>\n",
       "      <th>VWN</th>\n",
       "      <th>STRM</th>\n",
       "      <th>STRN</th>\n",
       "      <th>SA</th>\n",
       "      <th>SB</th>\n",
       "      <th>Run1 (ms)</th>\n",
       "      <th>Run2 (ms)</th>\n",
       "      <th>Run3 (ms)</th>\n",
       "      <th>Run4 (ms)</th>\n",
       "      <th>Mean_Runtime</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>115.26</td>\n",
       "      <td>115.87</td>\n",
       "      <td>118.55</td>\n",
       "      <td>115.80</td>\n",
       "      <td>116.3700</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>78.13</td>\n",
       "      <td>78.25</td>\n",
       "      <td>79.25</td>\n",
       "      <td>79.19</td>\n",
       "      <td>78.7050</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>79.84</td>\n",
       "      <td>80.69</td>\n",
       "      <td>80.76</td>\n",
       "      <td>80.97</td>\n",
       "      <td>80.5650</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>84.32</td>\n",
       "      <td>89.90</td>\n",
       "      <td>86.75</td>\n",
       "      <td>85.58</td>\n",
       "      <td>86.6375</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>115.13</td>\n",
       "      <td>121.98</td>\n",
       "      <td>122.73</td>\n",
       "      <td>114.81</td>\n",
       "      <td>118.6625</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   MWG  NWG  KWG  MDIMC  NDIMC  MDIMA  NDIMB  KWI  VWM  VWN  STRM  STRN  SA  \\\n",
       "0   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "1   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "2   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "3   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "4   16   16   16      8      8      8      8    2    1    1     0     1   0   \n",
       "\n",
       "   SB  Run1 (ms)  Run2 (ms)  Run3 (ms)  Run4 (ms)  Mean_Runtime  \n",
       "0   0     115.26     115.87     118.55     115.80      116.3700  \n",
       "1   1      78.13      78.25      79.25      79.19       78.7050  \n",
       "2   0      79.84      80.69      80.76      80.97       80.5650  \n",
       "3   1      84.32      89.90      86.75      85.58       86.6375  \n",
       "4   0     115.13     121.98     122.73     114.81      118.6625  "
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [],
   "source": [
    "data = data.drop(['Run1 (ms)', 'Run2 (ms)', 'Run3 (ms)','Run4 (ms)'], axis = 1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>MWG</th>\n",
       "      <th>NWG</th>\n",
       "      <th>KWG</th>\n",
       "      <th>MDIMC</th>\n",
       "      <th>NDIMC</th>\n",
       "      <th>MDIMA</th>\n",
       "      <th>NDIMB</th>\n",
       "      <th>KWI</th>\n",
       "      <th>VWM</th>\n",
       "      <th>VWN</th>\n",
       "      <th>STRM</th>\n",
       "      <th>STRN</th>\n",
       "      <th>SA</th>\n",
       "      <th>SB</th>\n",
       "      <th>Mean_Runtime</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>116.3700</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>78.7050</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>80.5650</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>86.6375</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>118.6625</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   MWG  NWG  KWG  MDIMC  NDIMC  MDIMA  NDIMB  KWI  VWM  VWN  STRM  STRN  SA  \\\n",
       "0   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "1   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "2   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "3   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "4   16   16   16      8      8      8      8    2    1    1     0     1   0   \n",
       "\n",
       "   SB  Mean_Runtime  \n",
       "0   0      116.3700  \n",
       "1   1       78.7050  \n",
       "2   0       80.5650  \n",
       "3   1       86.6375  \n",
       "4   0      118.6625  "
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array(['MWG', 'NWG', 'KWG', 'MDIMC', 'NDIMC', 'MDIMA', 'NDIMB', 'KWI',\n",
       "       'VWM', 'VWN', 'STRM', 'STRN', 'SA', 'SB', 'Mean_Runtime'],\n",
       "      dtype=object)"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "np.array(data.columns)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>MWG</th>\n",
       "      <th>NWG</th>\n",
       "      <th>KWG</th>\n",
       "      <th>MDIMC</th>\n",
       "      <th>NDIMC</th>\n",
       "      <th>MDIMA</th>\n",
       "      <th>NDIMB</th>\n",
       "      <th>KWI</th>\n",
       "      <th>VWM</th>\n",
       "      <th>VWN</th>\n",
       "      <th>STRM</th>\n",
       "      <th>STRN</th>\n",
       "      <th>SA</th>\n",
       "      <th>SB</th>\n",
       "      <th>Mean_Runtime</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>116.3700</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>78.7050</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>80.5650</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>86.6375</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>118.6625</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   MWG  NWG  KWG  MDIMC  NDIMC  MDIMA  NDIMB  KWI  VWM  VWN  STRM  STRN  SA  \\\n",
       "0   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "1   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "2   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "3   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "4   16   16   16      8      8      8      8    2    1    1     0     1   0   \n",
       "\n",
       "   SB  Mean_Runtime  \n",
       "0   0      116.3700  \n",
       "1   1       78.7050  \n",
       "2   0       80.5650  \n",
       "3   1       86.6375  \n",
       "4   0      118.6625  "
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [],
   "source": [
    "x = data.iloc[:,0:-1].values\n",
    "y = data['Mean_Runtime'].values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "(241600, 14)\n",
      "<class 'numpy.ndarray'>\n",
      "(241600,)\n",
      "<class 'numpy.ndarray'>\n"
     ]
    }
   ],
   "source": [
    "print(x.shape)\n",
    "\n",
    "print(type(x))\n",
    "\n",
    "print(y.shape)\n",
    "\n",
    "print(type(y))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn import preprocessing\n",
    "scaler = preprocessing.StandardScaler()\n",
    "x = scaler.fit_transform(x)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [],
   "source": [
    "x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.3, random_state = 42)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'numpy.ndarray'>\n",
      "(169120, 14)\n",
      "<class 'numpy.ndarray'>\n",
      "(72480, 14)\n"
     ]
    }
   ],
   "source": [
    "print(type(x_train))\n",
    "\n",
    "print(x_train.shape)\n",
    "\n",
    "print(type(x_test))\n",
    "\n",
    "print(x_test.shape)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [],
   "source": [
    "theta = np.zeros([15,1])\n",
    "\n",
    "m = len(x_train)\n",
    "\n",
    "ones = np.ones((m,1))\n",
    "\n",
    "x_train = np.hstack((ones, x_train))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [],
   "source": [
    "m1 = len(x_test)\n",
    "\n",
    "ones1 = np.ones((m1,1))\n",
    "\n",
    "x_test = np.hstack((ones1, x_test))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {},
   "outputs": [],
   "source": [
    "def costfunction(X, Y, theta):\n",
    "    \n",
    "    error = np.dot(X, theta) - Y\n",
    "    \n",
    "    return np.sqrt(np.sum(np.power(error, 2)) / (2*m))\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [],
   "source": [
    "y_train = y_train.reshape(len(y_train),1)\n",
    "y_test = y_test.reshape(len(y_test),1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "302.542457900703"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "costfunction(x_train, y_train, theta)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {},
   "outputs": [],
   "source": [
    "\n",
    "def gradient_descent(X, Y, B, alpha, iterations):\n",
    "    \n",
    "    rmse_history_train = []\n",
    "    \n",
    "    rmse_history_test = []\n",
    "    \n",
    "    m = len(Y)\n",
    "    \n",
    "    for iteration in range(iterations):\n",
    "        \n",
    "        h = X.dot(B)\n",
    "        \n",
    "        loss = h - Y\n",
    "        \n",
    "        gradient = X.T.dot(loss) / m\n",
    "        \n",
    "        B = B - alpha * gradient\n",
    "        \n",
    "        rmse_train = costfunction(X, Y, B)\n",
    "        \n",
    "        rmse_history_train.append(rmse_train)\n",
    "        \n",
    "        \n",
    "        rmse_test = costfunction(x_test, y_test, B)\n",
    "        \n",
    "        rmse_history_test.append(rmse_test)\n",
    "    \n",
    "        \n",
    "        \n",
    "        #if len(rmse_history_train) > 1:\n",
    "        \n",
    "            #if rmse_history_train[iteration-1] - rmse_history_train[iteration] < threshold:\n",
    "                \n",
    "                #break\n",
    "        \n",
    "    return B, rmse_history_train, rmse_history_test\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "###### $H(\\Theta)$ = 217.36268932 + 141.35 MWG + 130.84 NWG + 40.43 KWG - 130.77  MDIMC - 128.51  NDIMC + 8.91 MDIMA + 10.15 NDIMB +  11.85 KWI -2.55 VWM -5.72 VWN -4.50 STRM + 0.17 STRN + 19 SA + 23 SB"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {},
   "outputs": [],
   "source": [
    "B1,  rmse_history_train1, rmse_history_test1 = gradient_descent(x_train, y_train, theta, 0.0001, 2000)\n",
    "\n",
    "B2,  rmse_history_train2, rmse_history_test2 = gradient_descent(x_train, y_train, theta, 0.001, 2000 )\n",
    "\n",
    "B3,  rmse_history_train3, rmse_history_test3 = gradient_descent(x_train, y_train, theta, 0.01, 2000)\n",
    "\n",
    "B4,  rmse_history_train4, rmse_history_test4 = gradient_descent(x_train, y_train, theta, 0.1, 2000)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 86,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(rmse_history_train1,  label='alpha = 0.0001')\n",
    "\n",
    "plt.plot(rmse_history_train2,  label ='alpha = 0.001')\n",
    "\n",
    "plt.plot(rmse_history_train3,  label ='alpha = 0.01')\n",
    "\n",
    "plt.plot(rmse_history_train4,  label ='alpha = 0.1')\n",
    "\n",
    "\n",
    "plt.legend()\n",
    "\n",
    "plt.title('RMSE of training data with various alphas with no threshold\\n\\n')\n",
    "\n",
    "plt.xlabel('Number of Iterations\\n\\n')\n",
    "\n",
    "plt.ylabel('RMSE value\\n\\n')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 88,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(rmse_history_test1,  label='alpha = 0.0001')\n",
    "\n",
    "plt.plot(rmse_history_test2,  label ='alpha = 0.001')\n",
    "\n",
    "plt.plot(rmse_history_test3,  label ='alpha = 0.01')\n",
    "\n",
    "plt.plot(rmse_history_test4,  label ='alpha = 0.1')\n",
    "\n",
    "plt.legend()\n",
    "\n",
    "plt.title('RMSE of testing data with various alphas with no threshold\\n\\n')\n",
    "\n",
    "plt.xlabel('Number of Iterations\\n\\n')\n",
    "\n",
    "plt.ylabel('RMSE value\\n\\n')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 85,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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SLhu5Om3N7IvlDovx5hQVdLW/OOQYWUcMryUmkoFa+n/ultT3NNibaC3bdvGWWedxR133MGVV17ZNr2goIBp06bxwx/+kMWLF/Poo4/GLT9q1CguvfRSLr30UqZMmcKiRYs+cJlKSkrahufNm8czzzzDyy+/THFxMSeeeGLS/pwHDRrUNpybm0tLS8sHLofIQKAALVnNzKqBPSE8FwGfxF8Y+DxwLjAHuAh4OCzySHj8cpj+XG+2f+5t+bk5HDysjIOHlXEmI9vG79zTysq6ZpZvamTZBt8M5K3abTz+1npcJFiPryxuC9QHh3A9sbpETUFEekh5eTm33347s2bN4oorroibdu2113LCCSd0qPV98sknOfnkk8nPz2fDhg00NDQwevRoli5d2u3tlpWV0djYmHL6tm3bGDp0KMXFxSxdupRXXnklvScmIp1SgJZsNxL4RWgHnQM86Jx7zMzeBuaY2feAvwH3hPnvAX5pZivwNc8XZKLQva0wP5cjRg3miFGD48a37G7l3bomVmxqYvmmRpZvbOKdjY089faGthrrHINxFcUcHIJ1rNb6oGElFBfokCCSrqOPPpqjjjqKOXPmMGPGjLbxkydPjut9I+app57iqquuorCwEIBbbrmFESNGsHTp0g5toG+44QbOPffcDuuorKzk+OOPZ8qUKcycOZMzzzwzbvrpp5/OXXfdxYc+9CEOO+wwjjnmmJ56uiICWB+unBPpEdOnT3fz58/PdDF61a69rbxX38zyjU0s39TEuyFgv1ff3NbGGvzFi4cMK+WQcNHiIcN8zXVZobrbk+yxZMkSJk1KdimE9IZk+9vMFjjnpmeoSCIZp+omkQFgUF4uh48YzOEj4musfRvrHawItdXLN/nbX95tYPfe9l5BRpYXtjUBidZaqx9rEREZiBSgRQYw38ba1zKfPqV9fKxXkOWhpnpFCNe/fe19Wva092NdXTYohOlSDh5e1jZcWTooydZEJF0NDQ2cfPLJHcY/++yzHdpWi8iBowAtIh1EewU55YjhbeP37fP9WEfbWC/f1MTc19fStGtv23wVJQUcXF3KQSGcH1RdwsHDShlVXkROTrKeBkUkmcrKyra+nkUkeyhAi0i35eQYYyuKGVsR34+1c44N23e2BepYk5AnFq1n6472vzQvys9lYnUJB1WXclB1CNfDSqipVM8gIiLS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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(rmse_history_train1, label = 'RMSE_train')\n",
    "plt.plot(rmse_history_test1, label = 'RMSE_test')\n",
    "\n",
    "plt.legend()\n",
    "\n",
    "plt.title('RMSE of testing and testing and testing data with alpha = 0.0001 (just to see how train and test errors are changing\\n\\n\\)')\n",
    "\n",
    "plt.xlabel('Number of Iterations\\n\\n')\n",
    "\n",
    "plt.ylabel('RMSE value\\n\\n')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {},
   "outputs": [],
   "source": [
    "y_pred_test1 = np.dot(x_test, B1)\n",
    "y_pred_test2 = np.dot(x_test, B2)\n",
    "y_pred_test3 = np.dot(x_test, B3)\n",
    "y_pred_test4 = np.dot(x_test, B4)\n",
    "\n",
    "y_pred_train1 = np.dot(x_train, B1)\n",
    "y_pred_train2 = np.dot(x_train, B2)\n",
    "y_pred_train3 = np.dot(x_train, B3)\n",
    "y_pred_train4 = np.dot(x_train, B4)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics import mean_squared_error"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "metadata": {},
   "outputs": [],
   "source": [
    "rmse_train1 = mean_squared_error(y_train, y_pred_train1)\n",
    "rmse_train2 = mean_squared_error(y_train, y_pred_train2)\n",
    "rmse_train3 = mean_squared_error(y_train, y_pred_train3)\n",
    "rmse_train4 = mean_squared_error(y_train, y_pred_train4)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "metadata": {},
   "outputs": [],
   "source": [
    "rmse_test1 = mean_squared_error(y_test, y_pred_test1)\n",
    "rmse_test2 = mean_squared_error(y_test, y_pred_test2)\n",
    "rmse_test3 = mean_squared_error(y_test, y_pred_test3)\n",
    "rmse_test4 = mean_squared_error(y_test, y_pred_test4)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 53,
   "metadata": {},
   "outputs": [],
   "source": [
    "alpha_values = [0.0001,0.001,0.01,0.1]\n",
    "rmse_train_values = np.sqrt([rmse_train1,rmse_train2,rmse_train3,rmse_train4])\n",
    "rmse_test_values = np.sqrt([rmse_test1, rmse_test2, rmse_test3, rmse_test4])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([389.45977978, 292.8441518 , 285.01093359, 285.01091544])"
      ]
     },
     "execution_count": 54,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rmse_test_values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([388.30926077, 291.04403945, 283.35260907, 283.35260903])"
      ]
     },
     "execution_count": 55,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rmse_train_values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 74,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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vB7cw44kInvpuuuuY8GCBeTk5NC3b18GDhzIqaeeSo8ePQA49thjOeiggzjggAN4+OGHdx6XnZ3NqlWrWLRoEd26deP888/ngAMOYOjQoWzevBmAs88+mxdeeGFn+5tvvpnevXvTo0cP5s2bB8DKlSsZMmQIvXv35sILL6Rt27asWrWqzLxPP/00/fr1IycnhwsvvHBngWnQoAE33XQTBx98MDNmzCA7O5tbb72Vww8/nH//+9/MnTuX/v3707NnT4477jjWrFkDwIABA7j++us58sgjue+++6r+B4xu0a5yPbPSGHxgZ+7+/DhuWvgP+OZN6DIi7FgiMW/C/33Bl0vXV+l77t+qETcffUCZ+++44w4+//xz5s6dy9SpUxk1ahSff/75ztuSH3vsMZo0acLmzZvp27cvxx9/PBkZGbu9x7fffsuzzz7LI488wkknncSLL77I6aefXuKzmjZtykcffcSDDz7I3Xffzd///ncmTJjAUUcdxbhx43jzzTd3K3TFffXVVzz//PO8//77JCYmcvHFF/PMM89w5plnsmnTJrp3786tt966s31KSgrvvfceAD179uSBBx7gyCOP5KabbmLChAn86U9/AiK9wWnTplX+h7qH1BOqBlcP68LzPpjlSfvBpPFQsD3sSCJSBfr167fbczH3338/vXr1on///vz44498++23JY5p164dOTk5ABx00EEsWrSo1Pf+xS9+UaLNe++9x8knnwzA8OHDSU9PLzPb22+/zZw5c+jbty85OTm8/fbbfPfddwDEx8dz/PHH79Z+zJgxAKxbt461a9dy5JFHAnDWWWfx7rvvlmhXXdQTqgat0urxyyM6M27aGB7fdhfMfgwOvjDsWCIxrbweS02pX7/+zuWpU6fy1ltvMWPGDFJTUxkwYECpz80kJyfvXI6Pj995Oq6sdvHx8Tuvv/genM53d8466yxuv/32EvtSUlKIj48v83spT2Xb7S31hKrJrwZ04LN6B/NJ0oH41Nth85qwI4nIHmrYsCEbNmwodd+6detIT08nNTWVefPmMXPmzCr//MMPP5x//etfAEyaNGnntZrSDBo0iBdeeIEVK1YAsHr1ar7/vuJZFRo3bkx6ejrTp08H4KmnntrZK6oJKkLVpEFyAr8Z1oVrNoyBzetg2l1hRxKRPZSRkcFhhx1G9+7dGTt27G77hg8f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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(np.log(alpha_values), rmse_train_values, label = 'training_error')\n",
    "plt.plot(np.log(alpha_values), rmse_test_values, label = 'testing_error')\n",
    "plt.legend()\n",
    "\n",
    "plt.title('Alpha VS RMSE\\n')\n",
    "\n",
    "plt.xlabel('Alpha values\\n\\n')\n",
    "\n",
    "plt.ylabel('RMSE value\\n\\n')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "metadata": {},
   "outputs": [],
   "source": [
    "\n",
    "def gradient_descent_t(X, Y, B, alpha, iterations, threshold):\n",
    "    \n",
    "    rmse_history_train_t = []\n",
    "    \n",
    "    rmse_history_test_t = []\n",
    "    \n",
    "    m = len(Y)\n",
    "    \n",
    "    for iteration in range(iterations):\n",
    "        \n",
    "        h = X.dot(B)\n",
    "        \n",
    "        loss = h - Y\n",
    "        \n",
    "        gradient = X.T.dot(loss) / m\n",
    "        \n",
    "        B = B - alpha * gradient\n",
    "        \n",
    "        rmse_train = costfunction(X, Y, B)\n",
    "        \n",
    "        rmse_history_train_t.append(rmse_train)\n",
    "        \n",
    "        \n",
    "        rmse_test = costfunction(x_test, y_test, B)\n",
    "        \n",
    "        rmse_history_test_t.append(rmse_test)\n",
    "    \n",
    "        \n",
    "        \n",
    "        if len(rmse_history_train_t) > 1:\n",
    "        \n",
    "            if rmse_history_train_t[iteration-1] - rmse_history_train_t[iteration] < threshold:\n",
    "                \n",
    "                break\n",
    "        \n",
    "    return B, rmse_history_train_t, rmse_history_test_t\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "metadata": {},
   "outputs": [],
   "source": [
    "B5,  rmse_history_train_t5, rmse_history_test_t5 = gradient_descent_t(x_train, y_train, theta, 0.01, 2000, 0.000001 )\n",
    "\n",
    "B6,  rmse_history_train_t6, rmse_history_test_t6 = gradient_descent_t(x_train, y_train, theta, 0.01, 2000, 0.00001)\n",
    "\n",
    "B7,  rmse_history_train_t7, rmse_history_test_t7 = gradient_descent_t(x_train, y_train, theta, 0.01, 2000, 0.0001)\n",
    "\n",
    "B8,  rmse_history_train_t8, rmse_history_test_t8 = gradient_descent_t(x_train, y_train, theta, 0.01, 2000, 0.001)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {},
   "outputs": [],
   "source": [
    "y_pred_test5 = np.dot(x_test, B5)\n",
    "y_pred_test6 = np.dot(x_test, B6)\n",
    "y_pred_test7 = np.dot(x_test, B7)\n",
    "y_pred_test8 = np.dot(x_test, B8)\n",
    "\n",
    "y_pred_train5 = np.dot(x_train, B5)\n",
    "y_pred_train6 = np.dot(x_train, B6)\n",
    "y_pred_train7 = np.dot(x_train, B7)\n",
    "y_pred_train8 = np.dot(x_train, B8)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 63,
   "metadata": {},
   "outputs": [],
   "source": [
    "rmse_train5 = mean_squared_error(y_train, y_pred_train5)\n",
    "rmse_train6 = mean_squared_error(y_train, y_pred_train6)\n",
    "rmse_train7 = mean_squared_error(y_train, y_pred_train7)\n",
    "rmse_train8 = mean_squared_error(y_train, y_pred_train8)\n",
    "\n",
    "rmse_test5 = mean_squared_error(y_test, y_pred_test5)\n",
    "rmse_test6 = mean_squared_error(y_test, y_pred_test6)\n",
    "rmse_test7 = mean_squared_error(y_test, y_pred_test7)\n",
    "rmse_test8 = mean_squared_error(y_test, y_pred_test8)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {},
   "outputs": [],
   "source": [
    "threshold_values = [10**-5,10**-4, 10**-3, 10**-2]\n",
    "rmse_train_values_1 = np.sqrt([rmse_train5,rmse_train6,rmse_train7,rmse_train8])\n",
    "rmse_test_values_1 = np.sqrt([rmse_test5, rmse_test6, rmse_test7, rmse_test8])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 78,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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XowYMYKLL754fZ3Fz81qbU1d1v5RSQ+QjaYapknzO5ffrO1FxFOUH+WVPFxXsO2ZRfOj0vvccnVGxKWkCzjMLKcevgTefbl169x+L/jsD8uuLnwe1iOPPMLkyZN57rnniAiOPfZY/vznP7NgwQJ22GEHHnzwQSC7KW6/fv247rrreOKJJxg4cOBG9ZZ7RtbXvvY1brnlFg488EAuueSSJps+ceJE+vXrx/PPP88HH3zAQQcdxBFHHAHAc889t/65XbNnz+avf/0rv/rVr7jpppuYN28eF198MdOmTaOmpoYjjjiC+++/n+OPP77kc7NaU1OBdVzB9LVF64rnzcysCY888giPPPII++yzDwArV65k1qxZHHzwwVx44YVcfPHFHHPMMRx88MHN1lXqGVlLly5lxYoVHHjggQCceuqp/PGPf2yyPS+99NL6pxYvW7aMWbNm0a1bt42e27XTTjutvznv888/z7hx42g4T3/aaafx5z//meOPP77kc7NaU9nAiohGj4hMFzmMAN6JiJK/ZTIz67SaGAm1h4jg0ksv5dxzz91o3bRp03jooYe49NJLOeKII7j88subrKvUM7Ja8uyrhvb85Cc/4cgjj2y0/Mknn9zoGVaF803tp9Rzs1pTU5e13yxpzzTdD3iR7HZIL0g6pc1aZGa2hSh8HtaRRx7JL3/5S1auXAnAO++8w3vvvce8efPo1asXX/nKV7jwwguZPn36RttWoqamhj59+qx/rtZdd93VZPkjjzySn//856xduxaA119/nVWrVjW7n09+8pP86U9/YuHChdTV1XHnnXe22fOvijV1SPDgiPhGmv4a8HpEHC9pe+Bhst8qmZlZGYXPw/rsZz/LqaeeygEHHABkFyj89re/5Y033uCiiy6iS5cuVFdX8/Of/xyAc845h89+9rMMHjyYJ554oqL9TZw4kbPPPpttttmGcePG0a9fv7JlzzrrLGbPns2+++5LRDBo0CDuv3+ji6c3MnjwYK6++moOOeQQIoKjjz6a4447rtntWkPZ52FJeiEi9knTDwJ3R8Svi9dZaX4ellnH29qeh7Vy5Up69+4NZBd8zJ8/nxtuuKGDW1Veaz4Pa6mkY8juUH4Q8PVUWVegZ+s018zMWsuDDz7I1Vdfzbp169hpp5349a9/3dFNalVNBda5wI1kj/AYHxHvpuWHAQ+2dcPMzKxlTjrpJE466aRGy6ZMmdLot1KQXWV43333tWfTWkVTVwm+DhxVYvkUmn5Eh5mZdRJHHnnkRlcC5lXZwJJ0Y1MbRsT5rd8cM7PWFRFkd3OzzqSll+FD04cEvwG8AvyO7B59/sTNLFd69OjBokWLGDBggEOrE4kIFi1aRI8ePVq0XVOBNRj4EnAS2RN+JwH3RMSSTW6lmVk7Gjp0KHPnzsWP++l8evTowdChLXtGblPnsBaRPfDw5vQAxFOAVyVdHBG3b1ZLzczaQXV1daNbDFm+NTXCAkDSvmRh9RmyHwxPa+tGmZmZFWvqoosJwF4GOAgAABP0SURBVDFkz366C7g0Ita1V8PMzMwKNTXC+mfgb8De6fUv6aSlgEiPizczM2sXTQWWD/yamVmn0dRFF2+XWi6pCjgZKLnezMysLTT1eJG+ki6V9FNJRyjzbbLDhF9uvyaamZk1EVjA7cAngJeBs4BHgC8Cx0VE+9xLvgmShkl6QtJMSa9K+k5aPkrSM5JmSJoqaUzRdqMl1Un6Ypl695P0sqQ3JN2ohhN30raSHpU0K73XtH0vzcysQVOB9dGIODMi/p3ssvZa4JiImNE+TWvWOuC7EbE7sD/wj5L2AH4ETIiIUcDlaR5YfzjzGpq+F+LPgXOAXdOr4X6KlwCPR8SuwONp3szM2klTgbW2YSIi6oC3IqLyx1+2sYiYHxHT0/QKssvvhwAB9E3F+pHdVqrBt4F7gPdK1SlpMNA3Ip6O7EZXvwGOT6uPA25L07cVLDczs3bQ1FWCe0tanqYF9EzzDZe19y2/afuSNBzYB3gWGA9MkXQtWSAfmMoMAU4ADgVGl6lqCDC3YH5uWgbwkYiYD1lYStqudXthZmZNKTvCioiqiOibXn0iomvBdGcKq95ko6bxEbEcOA+4ICKGARcAE1PR64GL02ixbHUlllV8S2FJ56TzZlN97zIzs9bV1CHBTk9SNVlY3RER96bFZwAN03cDDRdd1AJ3SZpNdvHITZKKD+vNBQrvxjiUDYcU/zcdMmw4dLjRYcWIuCUiaiOidtCgQZvVNzMzayy3gZWu3psIzIyI6wpWzQPGpulDgVkAEbFzRAyPiOHAZOCbEXF/YZ3pkN8KSfun+r8K/D6tfoAsDEnvv8fMzNpNsze/7cQOAk4HXpbUcOXiZcDZwA2SugJryK74a5KkGemqQsgOKf4a6El2s9+H0/IfAr+T9HXg72SPXjEzs3aiTXnqozWvtrY2pk6d2tHNMDPLFUnTIqK21LrcHhI0M7OtiwPLzMxywYFlZma54MAyM7NccGCZmVkuOLDMzCwXHFhmZpYLDiwzM8sFB5aZmeWCA8vMzHLBgWVmZrngwDIzs1xwYJmZWS44sMzMLBccWGZmlgsOLDMzywUHlpmZ5YIDy8zMciGXgSVpmKQnJM2U9Kqk76TloyQ9I2mGpKmSxqTlx0l6qWD5p0rU2Setb3gtlHR9WnempAUF685q3x6bmVnXjm7AJloHfDcipkvqA0yT9CjwI2BCRDws6eg0Pw54HHggIkLSSOB3wG6FFUbECmBUw7ykacC9BUUmRcS32rJTZmZWXi4DKyLmA/PT9ApJM4EhQAB9U7F+wLxUZmXB5tukcmVJ2hXYDvhL67bczMw2VS4Dq5Ck4cA+wLPAeGCKpGvJDnceWFDuBOBqsiD6XDPVnkI2oioMthMlfRp4HbggIua0Vh/MzKx5uTyH1UBSb+AeYHxELAfOIwuTYcAFwMSGshFxX0TsBhwPfL+Zqk8G7iyY/wMwPCJGAo8Bt5VpzznpHNnUBQsWbGq3zMysBDUeROSHpGrgj8CUiLguLVsG9E/nqgQsi4i+JbZ9CxgdEQtLrNsbuDsiPl5mv1XA4ojo11T7amtrY+rUqS3ul5nZ1kzStIioLbUulyOsFEYTgZkNYZXMA8am6UOBWan8LmkbJO0LdAMWlan+FBqPrpA0uGD2WGDm5vbBzMxaJq/nsA4CTgdeljQjLbsMOBu4QVJXYA1wTlp3IvBVSWuB1cBJDeenJM2IiFEFdX8ZOLpof+dLOpbs6sTFwJmt3yUzM2tKbg8JdnY+JGhm1nJb3CFBMzPb+jiwzMwsFxxYZmaWCw4sMzPLBQeWmZnlggPLzMxywYFlZma54MAyM7NccGCZmVkuOLDMzCwXHFhmZpYLDiwzM8sFB5aZmeWCA8vMzHLBgWVmZrngwDIzs1xwYJmZWS44sMzMLBdyGViShkl6QtJMSa9K+k5aPkrSM5JmSJoqaUxafpyklwqWf6pMvU9K+msqN0PSdml5d0mTJL0h6VlJw9urr2Zmluna0Q3YROuA70bEdEl9gGmSHgV+BEyIiIclHZ3mxwGPAw9EREgaCfwO2K1M3adFxNSiZV8HlkTELpJOBq4BTmr9bpmZWTm5HGFFxPyImJ6mVwAzgSFAAH1TsX7AvFRmZUREWr5NKtcSxwG3penJwGGStOk9MDOzlsrrCGu9dHhuH+BZYDwwRdK1ZGF8YEG5E4Crge2AzzVR5a8k1QH3AD9IQTcEmAMQEeskLQMGAAtbuz9mZlZaLkdYDST1JguW8RGxHDgPuCAihgEXABMbykbEfRGxG3A88P0yVZ4WEXsBB6fX6Q27KlF2o1GapHPSObKpCxYs2NRumZnlTkTw3vI1THt7CS/8fUmb7EMbjpTli6Rq4I/AlIi4Li1bBvRP56oELIuIviW2fQsYHRFlR0iSzgRqI+JbkqYAV0bE05K6Au8Cg6KJP15tbW1MnVp8KszMLJ8igkWrPmTuktXMWfw+c5esZu6S95mT3t9ZspoP1tUDcODHBvAfZ++/SfuRNC0iakuty+UhwRRGE4GZDWGVzAPGAk8ChwKzUvldgDdTkO0LdAMWFdXZlSzsFqYwPAZ4LK1+ADgDeBr4IvBfTYWVmVneRARL31/LnCUFYbQ4e8/mV7N6bV2jbWp6VTO0phe7bd+Hw3f/CENrejKsphfDB27TJm3MZWABB5EdrntZ0oy07DLgbOCGFD5rgHPSuhOBr0paC6wGTmoIHEkzImIU0J3s/Fc1UEUWVrem7ScCt0t6A1gMnNzWHTQza23LigKpOJhWfdg4kPr26MqwbXvx0UHb8OmPD2JYTU+G1vRi6LbZe+/u7RshuT0k2Nn5kKCZtbcVa9Y2GhXNKRgdzV3yPivWrGtUvnf3rgxNITQshVDDKGlITU/69axu9z5scYcEzcy2Rqs+WNdodLT+XNLSbJS0bPXaRuV7datiWAqhMcNrGLZtrw0BVdOLvj27kqdf6DiwzMw6idUf1vHO0nQhw+INo6OGkdLiVR82Kt+jusv6UdE+w2o2Gi3V9KrOVSA1x4FlZtZO1qytY97S1euvrGt8xd1qFq78oFH5bl27MLR/T4Zu24sRQ/qtP1zXEEwDe3fbogKpOQ4sM7NW8uG6euYtXV1wyXfBKGnx+7y3onEgVVeJIf2z8Dl89+0KDtllwTSwd3e6dNl6Aqk5Diwzswqtravn3WVrsiAqcXHDu8vXUHgdW1UXsUP/Hgzt34txnxi04aKGFEzb9elBlQOpYg4sM7Okrj54d/maxj+MLQim+ctWU18QSF0Eg/tlI6IDPzawURgNrenJ9n170LUq1zcU6lQcWGa21aivD/53xZqSYTRnyfvMX7qGdQWJJMH2fXtkV9ntvO2G3yGlYNq+Xw+qHUjtxoFlZluM+vpg4coPGl3UUBhM7yxdzdq6xr893a5Pd4bW9GTfHWsYuveGS76H1vRkcP8edO9a1UG9sWIOLDOrWERQVx+sqw/q03R9Payrr6cuNkzX10NdWt/wqi+x7fpXBPUN69J88bbr19UHdQF19fXZRQ7L1jT6bdKH6X52DQb27sbQmuwqu6NGDG70A9kh/XvSo9qBlBcOrE6mvj74sC77B1d48jYKbg7feHnBdMGKxssLZ1q/zqD0xpWUr2S/xeXKLW+1v1GZeuqj+S/jwi/gkl/URV/OG38ZN9RdT1092bq6gvojqKvbUEdd8Rd5wb433pYN9dZH1pegZHAU7qdwXWe8Mc6223RjaE1Pdtu+D59J97Nr+C3SkP696NnNgbSlcGB1MnOXrObTP36io5thHayqi6iSsvcuoouga1UXukhUdSFbV5WV6dJFdO2itK7gldZVV3WhR3XR+jTdeFuo6tJlff3r16XyhdMN66rStl2rCuovbPdGbUv7kOjSBbqm/ZVre+G2pfbftUo+ZLcVcWB1Mv16VXPxUbutny/8TWDhxa+Nl6vk8kKFPy4sX0+Z8mXKUFGdzddTrnxxwbLtK1dXK/+NROGXaut+8a7/4k/rzGxjDqxOpl/Pas4b97GOboaZWafj6zHNzCwXHFhmZpYLDiwzM8sFB5aZmeWCA8vMzHLBgWVmZrngwDIzs1xwYJmZWS6o+J5t1jokLQDe3owqBgILW6k5HWlL6Qe4L53VltKXLaUfsHl92SkiBpVa4cDqpCRNjYjajm7H5tpS+gHuS2e1pfRlS+kHtF1ffEjQzMxywYFlZma54MDqvG7p6Aa0ki2lH+C+dFZbSl+2lH5AG/XF57DMzCwXPMIyM7NccGB1EpKulPSOpBnpdXSZckdJ+qukNyRd0t7trJSkCyWFpIFl1tcV9PWB9m5fS1TQlzMkzUqvM9q7fZWQ9H1JL6W/9yOSdihTrtN/Li3oS6f+XCT9WNJrqS/3SepfptxsSS+n/k5t73ZWogV92bzvr4jwqxO8gCuBC5spUwW8CXwU6Aa8COzR0W0v0c5hwBSy36ENLFNmZUe3szX6AmwL/C2916Tpmo5ud4l29i2YPh+4Oa+fSyV9ycPnAhwBdE3T1wDXlCk3u9y/o87yqqQvrfH95RFWvowB3oiIv0XEh8BdwHEd3KZS/g34P8CWcIK0ub4cCTwaEYsjYgnwKHBUezWuUhGxvGB2G3L82VTYl07/uUTEIxGxLs0+AwztyPZsjgr7stnfXw6szuVbaUj9S0k1JdYPAeYUzM9NyzoNSccC70TEi80U7SFpqqRnJB3fHm1rqQr70uk/kwaS/q+kOcBpwOVlinX6zwUq6ktuPpfkH4CHy6wL4BFJ0ySd045t2lTl+rLZn0nXzWiUtZCkx4DtS6z6HvBz4Ptk/3F+H/hXsg++URUltm33/1Nuph+XkR0eaM6OETFP0keB/5L0ckS82ZrtrEQr9KVTfCbQdF8i4vcR8T3ge5IuBb4FXFGibKf/XCrsS6f4XJrrRyrzPWAdcEeZag5Kn8l2wKOSXouIP7dNi8trhb5s9mfiwGpHEXF4JeUk3Qr8scSquWTnVBoMBea1QtNapFw/JO0F7Ay8KAmy9k2XNCYi3i2qY156/5ukJ4F9yI5vt6tW6MtcYFzB/FDgyTZpbDMq/e8L+A/gQUoEVmf/XEoo15dO8bk01490McgxwGGRTvSUqKPhM3lP0n1kh9baPbBaoS+b//3V0Sfr/Fp/QnJwwfQFwF0lynQlO3m8MxtOWu7Z0W1vok+zKX2hQg3QPU0PBGbRCS8eqbAv2wJvpT7VpOltO7q9Jdq5a8H0t4HJef1cKuxLp/9cyM6p/Q8wqIky2wB9Cqb/H3BUR7d9E/uy2d9fHd5Rv9Z/mLcDLwMvAQ80BBiwA/BQQbmjgdfJ/q/3ex3d7mb6tP5LHqgFfpGmD0x9fTG9f72j27qpfUnz/wC8kV5f6+i2lmn/PcAr6b+vPwBD8vq5VNKXPHwuqV1zgBnpdXNavv7fPNkVdS+m16ud9d98JX1J85v1/eU7XZiZWS74KkEzM8sFB5aZmeWCA8vMzHLBgWVmZrngwDIzs1xwYJm1EkkDCu50/m7B3feXSvqfNtjfOEmlfmDe1DZPSqotsfxMST9thTa1Sj1mpTiwzFpJRCyKiFERMQq4Gfi3ND0KqG9ue0m+84xZExxYZu2jStKtkl5Nz3DqCetHPP8i6U/AdyQNknSPpOfT66BUbmzB6O0FSX1Svb0lTU7PIrpD6T5Skg5L5V5ON1PuXtwgSV+T9Hra90El1ndJz2LqX7DsDUkfkfR5Sc+mfTwm6SMltv+1pC8WzK8smL4o9e8lSRPSsm0kPSjpRUmvSDppE//WtoVyYJm1j12Bn0XEnsBS4MSCdf0jYmxE/CtwA9nIbHQq84tU5kLgH9OI7WBgdVq+DzAe2IPsrggHSeoB/Bo4KSL2IrslznmFjZE0GJhAFlSfSds3EhH1wO+BE9I2nwRmR8T/Ak8B+0fEPmSPifg/lf4hJB2R/h5jyEaf+0n6NNntfeZFxN4RMQL4z0rrtK2DA8usfbwVETPS9DRgeMG6SQXThwM/lTSD7BZdfdNo6r+B6ySdTxZwDc8eei4i5qZwmZHq/UTa3+upzG3Ap4va80ngyYhYENmziSZR2iSgYaRzckG5ocAUSS8DFwF7NvcHKHBEer0ATAd2Iwuwl4HDJV0j6eCIWNaCOm0r4MAyax8fFEzX0fhJCasKprsABzScC4uIIRGxIiJ+CJwF9ASekbRbE/WWeoxDKZXcl+1pYBdJg4DjgXvT8p8AP00juHOBHiW2XZf6QzpU2S0tF3B1QR93iYiJKWD3IwuuqyWVe2aXbaUcWGadyyNkz3cCQNKo9P6xiHg5Iq4BppKNSsp5DRguaZc0fzrwp6IyzwLj0pWN1cCXSlUU2c1G7wOuA2ZGxKK0qh/wTpo+o0w7ZpMFEGRPlq1O01OAf5DUO/VtiKTtJO0AvB8RvwWuBfZtoo+2FfJVSWady/nAzyS9RPbv88/AN4Dxkg4hG0X9D9kTXQ8oVUFErJH0NeDudOXh82RXLRaWmS/pSrIR1HyyQ3NVZdo0KdVxZsGyK1P975A9En3nEtvdCvxe0nPA46SRZEQ8Iml34Ol0jchK4CvALsCPJdUDayk672bmu7WbmVku+JCgmZnlggPLzMxywYFlZma54MAyM7NccGCZmVkuOLDMzCwXHFhmZpYLDiwzM8sFB5aZmeWCA8vMzHLBgWVmZrngwDIzs1xwYJmZWS44sMzMLBccWGZmlgsOLDMzywUHlpmZ5YIDy8zMcsGBZWZmueDAMjOzXHBgmZlZLjiwzMwsFxxYZmaWCw4sMzPLBQeWmZnlggPLzMxywYFlZma54MAyM7NccGCZmVkuOLDMzCwXHFhmZpYL/x8O7ICs47LCMQAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(np.log10(threshold_values), rmse_train_values_1, label = 'training_error')\n",
    "plt.plot(np.log10(threshold_values), rmse_test_values_1, label = 'testing_error')\n",
    "\n",
    "plt.legend()\n",
    "\n",
    "plt.title('Threshold VS RMSE\\n\\n')\n",
    "\n",
    "plt.xlabel('Threshold values\\n\\n')\n",
    "\n",
    "plt.ylabel('RMSE value\\n\\n')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 75,
   "metadata": {},
   "outputs": [],
   "source": [
    "B_f, rmse_train_f, rmse_test_f = gradient_descent_t(x_train, y_train, theta, 0.001, 2000, 0.0001 )"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 83,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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Ynj++eeDHZI5gSxp1zKx0ZE8f20/Lnp6Fje+Mp/3f3kKrZIbBDssY0wt1bFjRxYtWnTUsD179jBy5Mhjpv3yyy+POd3MhBZL2rVQSlw9XrquPxc//S0/f3keU35xCgmxdj9aY0zVpKSk1KoqchM44dx7PKR1aBLPc6P78mPGfm6duJBDhcXBDskYY0yQWdKuxU7p0JiHL+3BzLW7uePt7ym2m4sYY0ydZtXjtdxP+7ZiV04e/5i6isZx9fjjeSfbPWqNMaaOsqQdAn4xrD0ZOfm8OGs9TRLqcYudw22MMXWSVY+HABHhj+d24YKeLXj4fyt5e/7mYIdkjPFU937aAI899hgHDhw4/L4q99g2dZsl7RBRcg730A6NufvdpXy1cmewQzLGENikXZV7bAda6XtlqyrFxVXr+FrV+2ybwLGkHUJioiJ49pq+dGmewK2vL2Tu+mNuQmaMqWG+99O+8847+ec//0n//v3p0aMH999/PwD79+/n3HPPpWfPnnTr1o3JkyfzxBNPsG3bNkaMGMGIESOAqt1je968efTo0YPBgwdz55130q1bt3JjKyoq4s477zwcz3PPPQe4G5n43ve7ZH233norffr0YfPmzUyaNInu3bvTrVs37rrrrsPLLH3fbVOzrE07xMTVi+Kl6/tz2XOz+fnL85h440C7apoxAP+7G3YsDewym3WHsx+ucBLf+2l/9tlnTJkyhblz56KqXHDBBcyYMYOMjAxatGjBxx9/DLgbiSQmJvLoo4/y9ddf07hx42OWW949tq+//nrGjx/PKaecwt13V3xfowkTJpCYmMi8efPIz89nyJAhjBo1CoC5c+cevu/3hg0bWLVqFS+99BJPP/0027Zt46677mLBggUkJyczatQo3n//fS666KIy77ttao6VtENQ47h6vHHjIBo1jGHMi3NZsT072CEZY3B32frss8/o3bs3ffr0YeXKlaxZs4bu3bvzxRdfcNddd/HNN9+QmJhY6bLKusd2VlYWOTk5nHLKKQBcddVVlcbz6quv0qtXLwYOHMiePXsO38+79H2/27Rpc/iGJvPmzWP48OGkpqYSFRXF1Vdfffj+2WXdd9vUHCtph6hmibG8fuNALntuNqNf+I7JNw+mQ5O4YIdlTPBUUiKuCarKPffcw80333zMuAULFvDJJ59wzz33MGrUKMaNG1fhssq6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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(rmse_train_f, label = 'training_error')\n",
    "plt.plot(rmse_test_f, label = 'testing_error')\n",
    "\n",
    "plt.legend()\n",
    "\n",
    "plt.title('RMSE VS Iterations with optimal alpha = 0.001 and optimal threshold = 0.0001\\n\\n')\n",
    "\n",
    "plt.xlabel('Iterations \\n\\n')\n",
    "\n",
    "plt.ylabel('RMSE value\\n\\n')\n",
    "\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 94,
   "metadata": {},
   "outputs": [],
   "source": [
    "p_f = np.dot(x_test, B_f)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 95,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "292.84415180417636"
      ]
     },
     "execution_count": 95,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "np.sqrt(mean_squared_error(y_test, p_f))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 96,
   "metadata": {},
   "outputs": [],
   "source": [
    "p_f_i = np.dot(x_test, theta)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 97,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "428.8315857028381"
      ]
     },
     "execution_count": 97,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "np.sqrt(mean_squared_error(y_test, p_f_i))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 104,
   "metadata": {},
   "outputs": [],
   "source": [
    "pred = np.dot(x_train, B_f)\n",
    "pred1 = np.dot(x_test, B_f)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 103,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "291.04403945056913"
      ]
     },
     "execution_count": 103,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "np.sqrt(mean_squared_error(y_train, pred))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 105,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "292.84415180417636"
      ]
     },
     "execution_count": 105,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "np.sqrt(mean_squared_error(y_test, pred1))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Logistic Part"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 416,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count    241600.000000\n",
       "mean        217.571953\n",
       "std         368.750161\n",
       "min          13.317500\n",
       "25%          40.667500\n",
       "50%          69.790000\n",
       "75%         228.387500\n",
       "max        3341.507500\n",
       "Name: Mean_Runtime, dtype: float64"
      ]
     },
     "execution_count": 416,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data['Mean_Runtime'].describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 419,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x1ff2778fc50>"
      ]
     },
     "execution_count": 419,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "data['Mean_Runtime'].hist(bins = 50)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 849,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "87821"
      ]
     },
     "execution_count": 849,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(data_l)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 439,
   "metadata": {},
   "outputs": [],
   "source": [
    "data_0 = data[(data['Mean_Runtime']<70)]\n",
    "\n",
    "data_1 = data[(data['Mean_Runtime']>70)]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 440,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "121124\n",
      "120471\n"
     ]
    }
   ],
   "source": [
    "print(len(data_0))\n",
    "\n",
    "print(len(data_1))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 441,
   "metadata": {},
   "outputs": [],
   "source": [
    "data1 = data.copy()\n",
    "data1['Mean_Runtime'] = np.where(data1['Mean_Runtime'].between(0,70), 0, data1['Mean_Runtime'])\n",
    "data1['Mean_Runtime'] = np.where(data1['Mean_Runtime'].between(70,4000), 1, data1['Mean_Runtime'])\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 446,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.0    121129\n",
       "1.0    120471\n",
       "Name: Mean_Runtime, dtype: int64"
      ]
     },
     "execution_count": 446,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data1['Mean_Runtime'].value_counts()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 447,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>MWG</th>\n",
       "      <th>NWG</th>\n",
       "      <th>KWG</th>\n",
       "      <th>MDIMC</th>\n",
       "      <th>NDIMC</th>\n",
       "      <th>MDIMA</th>\n",
       "      <th>NDIMB</th>\n",
       "      <th>KWI</th>\n",
       "      <th>VWM</th>\n",
       "      <th>VWN</th>\n",
       "      <th>STRM</th>\n",
       "      <th>STRN</th>\n",
       "      <th>SA</th>\n",
       "      <th>SB</th>\n",
       "      <th>Mean_Runtime</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>16</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>8</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   MWG  NWG  KWG  MDIMC  NDIMC  MDIMA  NDIMB  KWI  VWM  VWN  STRM  STRN  SA  \\\n",
       "0   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "1   16   16   16      8      8      8      8    2    1    1     0     0   0   \n",
       "2   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "3   16   16   16      8      8      8      8    2    1    1     0     0   1   \n",
       "4   16   16   16      8      8      8      8    2    1    1     0     1   0   \n",
       "\n",
       "   SB  Mean_Runtime  \n",
       "0   0           1.0  \n",
       "1   1           1.0  \n",
       "2   0           1.0  \n",
       "3   1           1.0  \n",
       "4   0           1.0  "
      ]
     },
     "execution_count": 447,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data1.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 888,
   "metadata": {},
   "outputs": [],
   "source": [
    "def sigmoid(X, theta):\n",
    "    z = np.dot(X, theta)\n",
    "    return 1 / (1 + np.exp(-z))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 455,
   "metadata": {},
   "outputs": [],
   "source": [
    "def costfunction_lr(X, Y, theta):\n",
    "    \n",
    "    m_lr = len(Y)\n",
    "    \n",
    "    predictions_lr = sigmoid(X,theta)\n",
    "    \n",
    "    error = (-Y * np.log(predictions)) - ((1-Y)*np.log(1-predictions))\n",
    "    \n",
    "    cost_lr = 1/m_lr * sum(error)\n",
    "    \n",
    "    return cost_lr"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 454,
   "metadata": {},
   "outputs": [],
   "source": [
    "\n",
    "def gradient_descent_lr(X, Y, B, alpha, iterations, threshold):\n",
    "    \n",
    "    cost_history = []\n",
    "\n",
    "    m = len(Y)\n",
    "    \n",
    "    for iteration in range(iterations):\n",
    "        \n",
    "        h = sigmoid(X,theta)\n",
    "        \n",
    "        loss = h - Y\n",
    "        \n",
    "        gradient = X.T.dot(loss) / m\n",
    "        \n",
    "        B = B - alpha * gradient\n",
    "        \n",
    "        cost = costfunction_lr(X, Y, B)\n",
    "        \n",
    "        cost_history.append(cost)\n",
    "        \n",
    "        rmse_history.append(rmse)\n",
    "        \n",
    "        if len(cost_history) > 1:\n",
    "        \n",
    "            if cost_history[iteration-1] - cost_history[iteration] < threshold:\n",
    "                \n",
    "                break\n",
    "        \n",
    "    return B_lr, cost_history_lr\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 458,
   "metadata": {},
   "outputs": [],
   "source": [
    "x_lr = data1.iloc[:,0:-1].values\n",
    "y_lr = data1['Mean_Runtime'].values"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 464,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "(241600, 14)\n",
      "(241600,)\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "(None, None)"
      ]
     },
     "execution_count": 464,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "print(x_lr.shape), print(y_lr.shape)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "theta = np.zeros([15,1])\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 469,
   "metadata": {},
   "outputs": [],
   "source": [
    "x_train_lr, x_test_lr, y_train_lr, y_test_lr = train_test_split(x_lr, y_lr, test_size = 0.3, random_state = 42)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 470,
   "metadata": {},
   "outputs": [
    {
     "ename": "ValueError",
     "evalue": "shapes (169120,14) and (9,1) not aligned: 14 (dim 1) != 9 (dim 0)",
     "output_type": "error",
     "traceback": [
      "\u001b[1;31m---------------------------------------------------------------------------\u001b[0m",
      "\u001b[1;31mValueError\u001b[0m                                Traceback (most recent call last)",
      "\u001b[1;32m<ipython-input-470-3e116d51c813>\u001b[0m in \u001b[0;36m<module>\u001b[1;34m\u001b[0m\n\u001b[1;32m----> 1\u001b[1;33m \u001b[0mB_lr\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mcost_history_lr\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mgradient_descent\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mx_train_lr\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0my_train_lr\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mtheta\u001b[0m\u001b[1;33m,\u001b[0m \u001b[1;36m0.01\u001b[0m\u001b[1;33m,\u001b[0m \u001b[1;36m1500\u001b[0m\u001b[1;33m,\u001b[0m \u001b[1;36m0.0001\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m",
      "\u001b[1;32m<ipython-input-208-83f5b8da98ca>\u001b[0m in \u001b[0;36mgradient_descent\u001b[1;34m(X, Y, B, alpha, iterations, threshold)\u001b[0m\n\u001b[0;32m      9\u001b[0m     \u001b[1;32mfor\u001b[0m \u001b[0miteration\u001b[0m \u001b[1;32min\u001b[0m \u001b[0mrange\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0miterations\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m     10\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m---> 11\u001b[1;33m         \u001b[0mh\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mX\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mdot\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mB\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m     12\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m     13\u001b[0m         \u001b[0mloss\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mh\u001b[0m \u001b[1;33m-\u001b[0m \u001b[0mY\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
      "\u001b[1;31mValueError\u001b[0m: shapes (169120,14) and (9,1) not aligned: 14 (dim 1) != 9 (dim 0)"
     ]
    }
   ],
   "source": [
    "B_lr, cost_history_lr = gradient_descent(x_train_lr, y_train_lr, theta, 0.01, 1500, 0.0001)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 471,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([[0.],\n",
       "       [0.],\n",
       "       [0.],\n",
       "       [0.],\n",
       "       [0.],\n",
       "       [0.],\n",
       "       [0.],\n",
       "       [0.],\n",
       "       [0.]])"
      ]
     },
     "execution_count": 471,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "theta"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "train.select_dtypes(include=[np.number])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "corr = numerical_features_train_df.corr()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 865,
   "metadata": {},
   "outputs": [],
   "source": [
    "li = [1000,500,250,125,72.5,10]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 873,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1"
      ]
     },
     "execution_count": 873,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "li[0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 871,
   "metadata": {},
   "outputs": [
    {
     "ename": "SyntaxError",
     "evalue": "invalid syntax (<ipython-input-871-cea79eba990a>, line 1)",
     "output_type": "error",
     "traceback": [
      "\u001b[1;36m  File \u001b[1;32m\"<ipython-input-871-cea79eba990a>\"\u001b[1;36m, line \u001b[1;32m1\u001b[0m\n\u001b[1;33m    for i in range(len(li5):\u001b[0m\n\u001b[1;37m                           ^\u001b[0m\n\u001b[1;31mSyntaxError\u001b[0m\u001b[1;31m:\u001b[0m invalid syntax\n"
     ]
    }
   ],
   "source": [
    "for i in range(len(li5):\n",
    "    if li[i]-li[i01] > 50:\n",
    "        print('shyam')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 900,
   "metadata": {},
   "outputs": [],
   "source": [
    "cost_history =[]\n",
    "rmse_history =[]\n",
    "\n",
    "    \n",
    "for i in range(10):\n",
    "    cost_history.append(i)\n",
    "    rmse_history.append(i)\n",
    "        \n",
    "    if len(rmse_history) >= 2:\n",
    "        \n",
    "        if rmse_history[i] - rmse_history[i-1] < 0.05:\n",
    "                \n",
    "            break"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 901,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]"
      ]
     },
     "execution_count": 901,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rmse_history"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
