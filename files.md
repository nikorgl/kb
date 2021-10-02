# Files

### Convert DVD (VOB files)
ffmpeg -i "concat:$(echo *.VOB|tr \  \|)" combined.mp4


### Rename video files with their creation dates
for i in *.MOV; do mv "$i" $(ffprobe -v quiet -select_streams v:0  -show_entries stream_tags=creation_time -of default=noprint_wrappers=1:nokey=1 "$i"  | awk '{print substr($1,1,20)}')mov ; done

### Rename photo files with their creation dates
for i in *.jpg; do mv "$i" $(exiv2 "$i" | grep timestamp | sed -e 's#.*\s:\s\(\)#\1#' -e 's/://g' -e 's/\s/_/g').jpg ; done

### Convert

#### Rotate images
for photo in *.jpg ; do convert $photo -rotate 90 $photo ; done

### Unoconv

#### Convert doc-file to pdf
unoconv -f pdf filename.docx
