# custom-listview-with-json-parsing-adapter
customlistview
package com.example.payilagam.customlistview.adapter;

import android.content.Context;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.ImageView;
import android.widget.TextView;

import com.example.payilagam.customlistview.R;
import com.example.payilagam.customlistview.imageloader.ImageLoader;
import com.example.payilagam.customlistview.model.CinemaItemBean;

import java.util.ArrayList;
import java.util.List;

/**
 * Created by Payilagam on 10/16/2015.
 */
public class CinemaAdapter extends ArrayAdapter {
    List<CinemaItemBean> resultValues;
    Context context;
    CinemaItemBean itemBean;
    ImageLoader imageLoader;
    public CinemaAdapter(Context context, int resource, List objects) {
        super(context, resource, objects);
        this.resultValues=objects;
        this.context=context;
        imageLoader=new ImageLoader(context);
    }

    public View getView(int position,View view,ViewGroup parent) {
        LayoutInflater inflater= (LayoutInflater) context.getSystemService(context.LAYOUT_INFLATER_SERVICE);
        View rowView=inflater.inflate(R.layout.cinema_list_item, null,true);
        TextView txtTitle=(TextView) rowView.findViewById(R.id.title);
        TextView txtRating= (TextView) rowView.findViewById(R.id.rating);
        TextView txtGenre= (TextView) rowView.findViewById(R.id.genre);
        TextView releaseYear= (TextView) rowView.findViewById(R.id.releaseYear);
        ImageView cinemaPic= (ImageView) rowView.findViewById(R.id.thumbnail);
        itemBean=resultValues.get(position);

        itemBean=resultValues.get(position);
        imageLoader.DisplayImage(itemBean.getThumbnailUrl(), cinemaPic);
        txtTitle.setText(itemBean.getTitle());
        txtRating.setText(String.valueOf(itemBean.getRating()));
        releaseYear.setText(String.valueOf(itemBean.getYear()));
        ArrayList<String> genreList=itemBean.getGenre();
        String genre="";
        for (int i=0;i<genreList.size();i++){
            genre=genre+genreList.get(i)+",";
        }
        txtGenre.setText(genre);
        return rowView;

    };
}
