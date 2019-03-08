# MultipleFilesDownloadASZipInMVC_Core
Multiple Files Download AS Zip In MVC_Core


 public FileResult Get(int id)
        {
            using (var memoryStream = new MemoryStream())
            {
                using (var ziparchive = new ZipArchive(memoryStream, ZipArchiveMode.Create, true))
                {
                    List<string> dd = new List<string>();
                    string file1 = @"22.png";
                    string file2 = @"33.png";
                    dd.Add(file1);
                    dd.Add(file2);
                    for (int i = 0; i < dd.Count; i++)
                    {
                        byte[] myByte = System.Text.ASCIIEncoding.Default.GetBytes(dd[i]);
                        var fileentry = ziparchive.CreateEntry(dd[i], CompressionLevel.Fastest);
                        using (var zipStream = fileentry.Open()) zipStream.Write(myByte, 0, myByte.Length);
                    }
                }
                var data = File(memoryStream.ToArray(), "application/zip", "Archeive.zip");
                return data;
            }

        
        }
        }
